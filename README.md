# LOTUS Skill Explorer — BUDS clustering (libero_object)

LOTUS fork의 trajectory **segmentation/clustering** 비교 연구용 인터랙티브 scatter explorer.
공개 LOTUS viewer(`khnuri-cell.github.io/lotus-viewer`)와 동일한 구조이며, 점 색상이
**BUDS(agglomerative, Ward) 클러스터**로 칠해진 버전입니다.

## 보는 법

- **GitHub Pages**: 이 repo를 Pages로 배포하면 루트 `index.html`이 진입점입니다.
- **로컬**: `python3 -m http.server 8765` 후 `http://localhost:8765` 접속.

## 구성

- `index.html` — 데이터셋 선택 진입 페이지
- `libero_object/index.html` — Plotly t-SNE scatter explorer
  - 점 1개 = trajectory segment (997개)
  - 색 = **BUDS 클러스터** (K=3, LOTUS와 동일 K에서 비교)
  - hover → 프레임 썸네일 + task/cluster/demo/구간 정보
  - click → 하단 패널에 frame grid + segment 비디오(h264)
  - 상단 필터: task / cluster 드롭다운
- `libero_object/frames/`, `frames_big/`, `videos/` — segment별 미디어

## 생성 파이프라인

raw LIBERO → DINOv2 per-frame feature → hierarchical agglomeration →
spectral clustering(LOTUS baseline) → BUDS 재클러스터링 색칠.
스크립트: `scripts/build_plotly_viewer.py --datasets libero_object --clustering buds --include-video`

## 데이터 출처

[LIBERO](https://github.com/Lifelong-Robot-Learning/LIBERO) (libero_object, 공개 데모 데이터셋).
