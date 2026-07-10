`pl3-hub` 기준으로 처음부터 끝까지 순서대로 정리했습니다.

## 1. GitHub에서 새 레포 생성

- Repository name: `pl3-hub`
- Public으로 생성 (GitHub Pages 무료 사용하려면 Public 필요, Private은 유료 플랜 필요)
- README 없이 비워둬도 되고, 있어도 무방

## 2. 로컬에서 레포 클론 + 파일 준비

```bash
git clone https://github.com/space-cap/pl3-hub.git
cd pl3-hub
```

지금 만든 `hub-pl3.html` 파일을 이 폴더에 넣고, **파일명을 반드시 `index.html`로** 변경합니다. (GitHub Pages는 루트의 `index.html`을 기본 진입점으로 찾습니다.)

```bash
mv hub-pl3.html index.html
```

## 3. CNAME 파일 생성

레포 루트에 확장자 없는 `CNAME` 파일을 만들고 내용은 딱 한 줄:

```
hub.pl3.kr
```

## 4. 커밋 + 푸시

```bash
git add index.html CNAME
git commit -m "hub.pl3.kr 초기 배포"
git push origin main
```

## 5. GitHub Pages 활성화

레포 → **Settings → Pages**
- Source: `Deploy from a branch`
- Branch: `main` / `/ (root)`
- Save

이 화면에서 Custom domain 칸에 `hub.pl3.kr`이 자동으로 채워져 있는지 확인 (CNAME 파일 덕분에 자동 인식됨). 안 채워져 있으면 직접 입력 후 Save.

## 6. Cloudflare DNS 설정

Cloudflare 대시보드 → pl3.kr → DNS → 레코드 추가:

| Type | Name | Content | Proxy |
|---|---|---|---|
| CNAME | `hub` | `space-cap.github.io` | 처음엔 **DNS only (회색 구름)** |

## 7. 확인 및 HTTPS 활성화

- GitHub Settings → Pages 화면에서 **"DNS check successful"** 표시될 때까지 대기 (보통 몇 분, 길면 몇 시간)
- 확인되면 **"Enforce HTTPS"** 체크
- 이후 Cloudflare에서 Proxy를 주황 구름(Proxied)으로 켜도 됨 (선택사항 — 켜면 Cloudflare의 캐싱/보안 기능 사용 가능)

## 8. 최종 확인

브라우저에서 `https://hub.pl3.kr` 접속해서 제대로 뜨는지 확인.

---

배포 끝나면 알려주세요. 잘 뜨는지 같이 확인하고, 그다음 `pl3-work`, `pl3-course` 만들 때는 이 순서를 거의 그대로 재사용하시면 됩니다.