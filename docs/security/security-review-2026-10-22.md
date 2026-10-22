# 2026-10-22 보안 검토 / Security review

## 범위와 판단

이미지 처리, TLS 신뢰 저장소, HTTP/ASGI 및 LLM 도구 의존성의 보고된 보안 버전을 갱신한다. 실제 공격 성공이나 외부 서비스 노출을 입증한 감사는 아니다.

스캐너: Trivy 0.74.0, 2026-10-22 DB 스냅샷, 개발 의존성 포함, 오프라인 재검사. 이전 버전 일치 112건 → 변경 후 0건. 동일 CVE의 여러 패키지·명세 출현을 포함한 수이며 실제 공격 경로 개수가 아니다.

## 수정 이유와 변경

Pillow 13.0.0, certifi 2026.10.19 및 호환되는 FastAPI/Starlette, Streamlit, LiteLLM, HTTP·암호화 하위 패치. MoviePy는 공식 97316f37f6a8d3843abfb53eba8f3bb0ea46a008 소스 아카이브로 고정한다. 이 커밋은 Pillow 상한과 제거된 비공개 텍스트 API 문제를 해결하며 2.2.1 태그 대비 13개 커밋/9개 파일을 포함한다. uv.lock에 아카이브 해시가 고정된다. legacy pip/Docker와 uv의 보안 제약을 함께 유지하고 직접 사용하는 toml을 명시한다. FFmpeg 빌드 차이에 따른 DASH 거부 진단을 허용하면서 실패 상태와 출력 부재를 계속 검증한다.

[MoviePy 공식 호환 수정](https://github.com/Zulko/moviepy/commit/97316f37f6a8d3843abfb53eba8f3bb0ea46a008) · [기존 릴리스 대비 전체 차이](https://github.com/Zulko/moviepy/compare/v2.2.1...97316f37f6a8d3843abfb53eba8f3bb0ea46a008) · [certifi 공지](https://github.com/certifi/python-certifi/security/advisories/GHSA-6q48-6c7w-9gw2)

## 남은 항목과 한계

공식 MoviePy 소스 커밋 사용은 PyPI 정식 릴리스만 사용하는 기존 설치 방식의 변경이다. 움직이는 master 브랜치나 resolver 강제 옵션을 쓰지 않는다. 다음 공식 호환 릴리스가 나오면 이 임시 소스 고정을 제거해야 한다. 실제 유료 외부 API·GPU·배포 컨테이너는 검증하지 않는다.

이번 PHP 두 CVE는 검토한 앱·배포 경로에 직접 사용하는 PHP 런타임이 없어 해당 패치를 추가하지 않았다. [PHP 공식 공지](https://www.php.net/archive/2026.php#2026-10-21-5). 운영 환경 전체의 무취약성 또는 침해 부재를 보장하는 결론은 아니다.

## 보고된 항목 전체

각 행의 링크는 개별 공지다. 원문 참고 링크와 변경 후 남은 항목 전체는 [JSON 보고서](security-findings-2026-10-22.json)에 포함한다.

| 명세·산출물 | 패키지 / 이전 버전 | 공지 | 처리 |
|---|---|---|---|
| requirements.txt | `litellm` 1.86.2 | [CVE-2026-84377](https://github.com/BerriAI/litellm/security/advisories/GHSA-3cv6-jpf6-8222) | 패치 또는 의존성 제거 |
| requirements.txt | `python-multipart` 0.0.27 | [CVE-2026-53537](https://github.com/Kludex/python-multipart/security/advisories/GHSA-vffw-93wf-4j4q) | 패치 또는 의존성 제거 |
| requirements.txt | `python-multipart` 0.0.27 | [CVE-2026-53538](https://github.com/Kludex/python-multipart/security/advisories/GHSA-6jv3-5f52-599m) | 패치 또는 의존성 제거 |
| requirements.txt | `python-multipart` 0.0.27 | [CVE-2026-53539](https://github.com/Kludex/python-multipart/security/advisories/GHSA-5rvq-cxj2-64vf) | 패치 또는 의존성 제거 |
| requirements.txt | `python-multipart` 0.0.27 | [CVE-2026-53540](https://github.com/Kludex/python-multipart/security/advisories/GHSA-v9pg-7xvm-68hf) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-111063](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-494j-54xm-rwp3) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-111064](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-5wr8-gcqf-gqf3) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-111065](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-6cjc-53gc-5rqm) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-111066](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-9xw5-w5jj-pvcg) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-111748](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-f9xw-jh8m-3mwq) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-111749](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-gx76-c99x-2c96) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-111750](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-pqxq-w44r-73xw) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54273](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-4fvr-rgm6-gqmc) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54274](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-xcgm-r5h9-7989) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54275](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-4m7w-qmgq-4wj5) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54276](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-hpj7-wq8m-9hgp) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54277](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-63hw-fmq6-xxg2) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54278](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-g3cq-j2xw-wf74) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54279](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-2fqr-mr3j-6wp8) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-54280](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-9x8q-7h8h-wcw9) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-59881](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-mq44-7p77-q5h7) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-69243](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-mfx4-hv73-q22v) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [CVE-2026-69244](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-cq5v-8q36-5273) | 패치 또는 의존성 제거 |
| uv.lock | `aiohttp` 3.14.0 | [GHSA-2g87-pp6c-29x5](https://github.com/aio-libs/aiohttp/security/advisories/GHSA-2g87-pp6c-29x5) | 패치 또는 의존성 제거 |
| uv.lock | `anyio` 4.13.0 | [CVE-2026-63374](https://github.com/agronholm/anyio/security/advisories/GHSA-82r6-8w77-94w6) | 패치 또는 의존성 제거 |
| uv.lock | `anyio` 4.13.0 | [CVE-2026-64847](https://github.com/agronholm/anyio/security/advisories/GHSA-5p39-cfhj-2xmp) | 패치 또는 의존성 제거 |
| uv.lock | `certifi` 2026.2.25 | [GHSA-6q48-6c7w-9gw2](https://github.com/certifi/python-certifi/security/advisories/GHSA-6q48-6c7w-9gw2) | 패치 또는 의존성 제거 |
| uv.lock | `cryptography` 49.0.0 | [CVE-2026-69247](https://github.com/pyca/cryptography/security/advisories/GHSA-g6cj-pr64-35w5) | 패치 또는 의존성 제거 |
| uv.lock | `fsspec` 2026.3.0 | [CVE-2026-104851](https://github.com/fsspec/filesystem_spec/security/advisories/GHSA-27vj-qcqg-25rc) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-67322](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-rwj8-pgh3-r573) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-67323](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-956x-8gvw-wg5v) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-67325](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-2f96-g7mh-g2hx) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-76217](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-hh9p-6wh2-4mfc) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-76218](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-9rj7-rf2p-w77r) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-76219](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-4gmw-gg2m-w46p) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-76220](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-wvpp-8hx9-p66j) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-76222](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-hmq2-w58f-27jc) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-78675](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-7833-fr7j-v32q) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-78676](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-284h-m62q-gf8w) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-78677](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-8mcc-hrx5-hvxc) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-78678](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-5xxx-qhh7-9287) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-78679](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-3wxw-xv34-2frg) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-87817](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-239g-whfq-7xj9) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [CVE-2026-87819](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-g5vv-9gxw-82hx) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-3f7w-8rr8-f37f](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-3f7w-8rr8-f37f) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-3rp5-jjmw-4wv2](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-3rp5-jjmw-4wv2) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-539m-9xh6-q6rr](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-539m-9xh6-q6rr) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-59cr-6r3x-644w](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-59cr-6r3x-644w) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-6p8h-3wgx-97gf](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-6p8h-3wgx-97gf) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-94p4-4cq8-9g67](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-94p4-4cq8-9g67) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-fjr4-x663-mwxc](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-fjr4-x663-mwxc) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-jm78-9fvv-mhgr](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-jm78-9fvv-mhgr) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-p538-c434-8v24](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-p538-c434-8v24) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-r9mr-m37c-5fr3](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-r9mr-m37c-5fr3) | 패치 또는 의존성 제거 |
| uv.lock | `gitpython` 3.1.50 | [GHSA-v396-v7q4-x2qj](https://github.com/gitpython-developers/GitPython/security/advisories/GHSA-v396-v7q4-x2qj) | 패치 또는 의존성 제거 |
| uv.lock | `litellm` 1.86.2 | [CVE-2026-84377](https://github.com/BerriAI/litellm/security/advisories/GHSA-3cv6-jpf6-8222) | 패치 또는 의존성 제거 |
| uv.lock | `multidict` 6.7.1 | [CVE-2026-104874](https://github.com/aio-libs/multidict/security/advisories/GHSA-54p9-h82j-f925) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112390](https://github.com/python-pillow/Pillow/security/advisories/GHSA-22hg-r758-rrw9) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112391](https://github.com/python-pillow/Pillow/security/advisories/GHSA-254f-3936-288h) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112392](https://github.com/python-pillow/Pillow/security/advisories/GHSA-27h8-gf7j-v5hc) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112393](https://github.com/python-pillow/Pillow/security/advisories/GHSA-332p-7hrc-92wf) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112394](https://github.com/python-pillow/Pillow/security/advisories/GHSA-4558-3h8r-v8xp) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112395](https://github.com/python-pillow/Pillow/security/advisories/GHSA-462x-pgg6-55fp) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112396](https://github.com/python-pillow/Pillow/security/advisories/GHSA-4rr5-89j8-mwwm) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112397](https://github.com/python-pillow/Pillow/security/advisories/GHSA-58r4-6rv3-gfh8) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112399](https://github.com/python-pillow/Pillow/security/advisories/GHSA-5xm2-6676-qcp9) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112400](https://github.com/python-pillow/Pillow/security/advisories/GHSA-65qm-jvmh-6pqg) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112401](https://github.com/python-pillow/Pillow/security/advisories/GHSA-74r2-7ff9-mjj2) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112402](https://github.com/python-pillow/Pillow/security/advisories/GHSA-7mwm-ghpf-9vrm) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112403](https://github.com/python-pillow/Pillow/security/advisories/GHSA-8g5g-8vmr-9782) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112404](https://github.com/python-pillow/Pillow/security/advisories/GHSA-c6hw-5grf-ff96) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112406](https://github.com/python-pillow/Pillow/security/advisories/GHSA-f2g6-542v-9j58) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112891](https://github.com/python-pillow/Pillow/security/advisories/GHSA-fc9g-5qg7-mf45) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112892](https://github.com/python-pillow/Pillow/security/advisories/GHSA-gg2r-wvfm-q9rx) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112893](https://github.com/python-pillow/Pillow/security/advisories/GHSA-j4m9-6w36-pw47) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112894](https://github.com/python-pillow/Pillow/security/advisories/GHSA-jg86-v3jv-hrpm) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112895](https://github.com/python-pillow/Pillow/security/advisories/GHSA-p4wg-p73j-c528) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112896](https://github.com/python-pillow/Pillow/security/advisories/GHSA-pchr-8j38-3x4p) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112897](https://github.com/python-pillow/Pillow/security/advisories/GHSA-q45j-58j2-45rg) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112898](https://github.com/python-pillow/Pillow/security/advisories/GHSA-rfgq-q3w2-pmv2) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112899](https://github.com/python-pillow/Pillow/security/advisories/GHSA-vx6w-vv9f-6gvg) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112900](https://github.com/python-pillow/Pillow/security/advisories/GHSA-w889-685w-c8fh) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112901](https://github.com/python-pillow/Pillow/security/advisories/GHSA-xgh8-jp6q-p5x8) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-112902](https://github.com/python-pillow/Pillow/security/advisories/GHSA-xvh5-g6gv-559v) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-25990](https://github.com/python-pillow/Pillow/security/advisories/GHSA-cfh3-3jmp-rvhc) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-40192](https://github.com/python-pillow/Pillow/security/advisories/GHSA-whj4-6x5x-4v2j) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-42308](https://github.com/python-pillow/Pillow/security/advisories/GHSA-wjx4-4jcj-g98j) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-42309](https://github.com/python-pillow/Pillow/security/advisories/GHSA-5xmw-vc9v-4wf2) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-42310](https://github.com/python-pillow/Pillow/security/advisories/GHSA-r73j-pqj5-w3x7) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-42311](https://github.com/python-pillow/Pillow/security/advisories/GHSA-cfh3-3jmp-rvhc) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-54058](https://github.com/python-pillow/Pillow/security/advisories/GHSA-62p4-gmf7-7g93) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-54059](https://github.com/python-pillow/Pillow/security/advisories/GHSA-8v84-f9pq-wr9x) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-54060](https://github.com/python-pillow/Pillow/security/advisories/GHSA-5x94-69rx-g8h2) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-55379](https://github.com/python-pillow/Pillow/security/advisories/GHSA-45hq-cxwh-f6vc) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-55380](https://github.com/python-pillow/Pillow/security/advisories/GHSA-phj9-mv4w-65pm) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-55798](https://github.com/python-pillow/Pillow/security/advisories/GHSA-4x4j-2g7c-83w6) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-59197](https://github.com/python-pillow/Pillow/security/advisories/GHSA-xj96-63gp-2gmr) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-59198](https://github.com/python-pillow/Pillow/security/advisories/GHSA-fj7v-r99m-22gq) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-59199](https://github.com/python-pillow/Pillow/security/advisories/GHSA-6r8x-57c9-28j4) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-59200](https://github.com/python-pillow/Pillow/security/advisories/GHSA-jjj6-mw9f-p565) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-59204](https://github.com/python-pillow/Pillow/security/advisories/GHSA-vjc4-5qp5-m44j) | 패치 또는 의존성 제거 |
| uv.lock | `pillow` 11.3.0 | [CVE-2026-59205](https://github.com/python-pillow/Pillow/security/advisories/GHSA-9hw9-ch79-4vh6) | 패치 또는 의존성 제거 |
| uv.lock | `python-multipart` 0.0.27 | [CVE-2026-53537](https://github.com/Kludex/python-multipart/security/advisories/GHSA-vffw-93wf-4j4q) | 패치 또는 의존성 제거 |
| uv.lock | `python-multipart` 0.0.27 | [CVE-2026-53538](https://github.com/Kludex/python-multipart/security/advisories/GHSA-6jv3-5f52-599m) | 패치 또는 의존성 제거 |
| uv.lock | `python-multipart` 0.0.27 | [CVE-2026-53539](https://github.com/Kludex/python-multipart/security/advisories/GHSA-5rvq-cxj2-64vf) | 패치 또는 의존성 제거 |
| uv.lock | `python-multipart` 0.0.27 | [CVE-2026-53540](https://github.com/Kludex/python-multipart/security/advisories/GHSA-v9pg-7xvm-68hf) | 패치 또는 의존성 제거 |
| uv.lock | `setuptools` 82.0.1 | [CVE-2026-59890](https://github.com/pypa/setuptools/security/advisories/GHSA-h35f-9h28-mq5c) | 패치 또는 의존성 제거 |
| uv.lock | `starlette` 1.2.1 | [CVE-2026-54282](https://github.com/Kludex/starlette/security/advisories/GHSA-jp82-jpqv-5vv3) | 패치 또는 의존성 제거 |
| uv.lock | `starlette` 1.2.1 | [CVE-2026-54283](https://github.com/Kludex/starlette/security/advisories/GHSA-82w8-qh3p-5jfq) | 패치 또는 의존성 제거 |
| uv.lock | `urllib3` 2.7.0 | [CVE-2026-97687](https://github.com/urllib3/urllib3/security/advisories/GHSA-8988-9cw3-xx77) | 패치 또는 의존성 제거 |
| uv.lock | `urllib3` 2.7.0 | [CVE-2026-97688](https://github.com/urllib3/urllib3/security/advisories/GHSA-gh4c-6fx4-qh6g) | 패치 또는 의존성 제거 |
| uv.lock | `urllib3` 2.7.0 | [CVE-2026-97689](https://github.com/urllib3/urllib3/security/advisories/GHSA-vxq7-64xx-v4gw) | 패치 또는 의존성 제거 |

## 반영 절차

기존 환경은 직접 바꾸지 않았다. 병합 후 새 환경에서 uv sync --frozen으로 반영하거나 새 컨테이너를 빌드한다. 사용자 파일과 설정을 보존하고 기존 환경에서 무조건 일괄 업그레이드하지 않는다.

## 검증

정확한 실행 명령, 결과와 미실행 검사는 이 PR 본문의 한국어·영어 검증 절에 기록한다. 위 건수는 스캐너가 지원한 명세 및 Java SBOM 범위의 스냅샷이다.
