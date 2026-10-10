# WOL 주소와 도구 요령

## 주소 형식 (한국어)
- 검색 (많이 나온 순): `https://wol.jw.org/ko/wol/s/r8/lp-ko?q=검색어&p=par&r=occ`
- 검색 (최신순): 위 주소의 `r=occ` → `r=newest`
- 성경 장 (연구용): `https://wol.jw.org/ko/wol/b/r8/lp-ko/nwtsty/책번호/장`
- 오늘의 성구 / 홈: `https://wol.jw.org/ko/wol/h/r8/lp-ko`
- 영어 연구용 성경 (연구 노트 확인용): `https://wol.jw.org/en/wol/b/r1/lp-e/nwtsty/책번호/장`

## 성경 책번호
창세기 1, 출애굽기 2, 레위기 3, 민수기 4, 신명기 5, 여호수아 6, 재판관기 7, 룻기 8, 사무엘상 9, 사무엘하 10, 열왕기상 11, 열왕기하 12, 역대기상 13, 역대기하 14, 에스라 15, 느헤미야 16, 에스더 17, 욥기 18, 시편 19, 잠언 20, 전도서 21, 솔로몬의 노래 22, 이사야 23, 예레미야 24, 애가 25, 에스겔 26, 다니엘 27, 호세아 28, 요엘 29, 아모스 30, 오바댜 31, 요나 32, 미가 33, 나훔 34, 하박국 35, 스바냐 36, 학개 37, 스가랴 38, 말라기 39,
마태 40, 마가 41, 누가 42, 요한 43, 사도행전 44, 로마 45, 고린도 전서 46, 고린도 후서 47, 갈라디아 48, 에베소 49, 빌립보 50, 골로새 51, 데살로니가 전서 52, 데살로니가 후서 53, 디모데 전서 54, 디모데 후서 55, 디도 56, 빌레몬 57, 히브리 58, 야고보 59, 베드로 전서 60, 베드로 후서 61, 요한 1서 62, 요한 2서 63, 요한 3서 64, 유다 65, 계시록 66

## 성경 페이지에서 구절과 각주를 가져오는 방법 (wol.jw.org 페이지 안에서 실행)
구절은 `span.v`이고, id에 `-장-절-` 형태가 들어 있다. 각주 링크는 href에 `/fn/`이 들어 있다.

```js
async function vv(b,c,vs){
  const h=await fetch(`/ko/wol/b/r8/lp-ko/nwtsty/${b}/${c}`).then(r=>r.text());
  const d=new DOMParser().parseFromString(h,'text/html'); let out=[];
  for(const v of vs){
    const sp=[...d.querySelectorAll('span.v')].filter(s=>new RegExp(`-${c}-${v}-`).test(s.id));
    const t=sp.map(s=>s.innerText).join(' ').replace(/\s+/g,' ');
    const fh=sp.flatMap(s=>[...s.querySelectorAll('a')].map(a=>a.getAttribute('href'))).filter(x=>x&&x.includes('/fn/'));
    const fn=await Promise.all(fh.map(u=>fetch(u).then(r=>r.text()).then(x=>{const dd=new DOMParser().parseFromString(x,'text/html');return (dd.querySelector('article')||dd.body).innerText.replace(/\s+/g,' ').replace('각주','').trim()})));
    out.push(`[${b}:${c}:${v}] ${t}${fn.length?' {각주: '+fn.join(' / ')+'}':''}`);
  }
  return out.join('\n');
}
// 예: await vv(19,118,[5,6])
```

## 요령
- 검색 결과 페이지의 본문은 `article` 요소 안에 있다.
- 결과 링크를 클릭했는데 페이지가 바뀌지 않으면, 링크의 href(`/ko/wol/d/r8/lp-ko/숫자`)로 직접 이동한다.
- 열린 기사에서 특정 표현의 앞뒤 문맥을 볼 때: `document.body.innerText`에서 그 표현의 위치를 찾아 앞뒤 1000자 정도를 잘라 읽는다.
- 「통찰」 항목은 주제어(예: "사탄", "탐식가", "여호와")로 검색하면 잘 나온다.
