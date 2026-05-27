# BUDS Skill Explorer — libero_object + libero_goal

LOTUS fork의 trajectory segmentation/clustering 비교 연구용 인터랙티브 scatter explorer.
점 색상이 **BUDS(agglomerative, Ward) 클러스터**로 칠해진 버전입니다.
공개 LOTUS viewer(`khnuri-cell.github.io/lotus-viewer`)와 동일 구조이며, 두 데이터셋을 한 사이트에서 봅니다.

## 보는 법

- **GitHub Pages**: repo를 Pages로 배포하면 루트 `index.html`이 진입점.
- **로컬**: `python3 -m http.server 8765` 후 `http://localhost:8765`.

## 구성

- `index.html` — 데이터셋 선택 진입 페이지 (libero_object, libero_goal)
- `libero_object/index.html` — 997 segments, 10 tasks, K=3
- `libero_goal/index.html` — 810 segments, 10 tasks, K=3
- 각 explorer:
  - 점 1개 = trajectory segment, 색 = **BUDS 클러스터** (LOTUS와 동일 K에서 비교)
  - hover → 프레임 썸네일 + task/cluster/demo/구간 정보
  - click → frame grid + segment 비디오(h264)
  - 상단 필터: task / cluster
- `<dataset>/frames/`, `frames_big/`, `videos/` — segment별 미디어

## 생성 파이프라인

raw LIBERO → DINOv2 per-frame feature → hierarchical agglomeration →
spectral clustering(LOTUS baseline, segmentation) → BUDS 재클러스터링 색칠.
스크립트: `scripts/build_plotly_viewer.py --datasets libero_object libero_goal --clustering buds --include-video`

LOTUS vs BUDS(+XSkill, CompILE) 정량 비교 metric은 `scripts/compare_clustering_methods.py` → `results/method_comparison/metrics.csv`.

## 데이터 출처

[LIBERO](https://github.com/Lifelong-Robot-Learning/LIBERO) (libero_object, libero_goal — 공개 데모 데이터셋).
