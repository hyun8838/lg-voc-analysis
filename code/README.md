# LG VOC 분석 코드

이 폴더에는 포트폴리오에 적힌 수집·전처리·빈도·연관어·감정어·브랜드 분석 범위의 공개용 노트북만 담았습니다. 게시글 원문, 수집 결과 CSV, API 키와 실행 출력은 포함하지 않습니다.

| 순서 | 노트북 | 내용 |
|---|---|---|
| 1 | [tistory_crawling.ipynb](tistory_crawling.ipynb) | Selenium으로 티스토리 글 수집. 게시일을 확인할 수 없으면 날짜를 비워 둠 |
| 2 | [youtube_script.ipynb](youtube_script.ipynb) | YouTube Data API로 영상 검색 후 한국어 자막 수집 |
| 3 | [data_pooling_preprocess.ipynb](data_pooling_preprocess.ipynb) | 출처별 자료 통합, 제목·노이즈·중복·길이 기준 적용, 분석 입력 생성 |
| 4 | [freq_analysis.ipynb](freq_analysis.ipynb) | 전체·연도·계절별 빈도와 3개년 변화 유형 |
| 5 | [keyword_analysis.ipynb](keyword_analysis.ipynb) | ‘미니’·‘핸디’ 등 연관어 계산·시각화 |
| 6 | [sent_analysis.ipynb](sent_analysis.ipynb) | 분석 대상 감정어 목록과 주변 어휘 분석 |
| 7 | [vacuum_network_brand.ipynb](vacuum_network_brand.ipynb) | 무선청소기 브랜드별 키워드·네트워크 분석 |

## 비공개 입력과 실행 범위

* Jupyter 환경에서 노트북을 실행합니다. 한국어 형태소 분석에는 Java와 KoNLPy의 Okt 실행 환경이 필요합니다. 티스토리 수집에는 Chrome과 호환되는 ChromeDriver를 준비하고 `CHROMEDRIVER_PATH`를 지정합니다. Python 패키지는 `requirements.txt`를 참고합니다.

* 수집·통합 노트북은 `LG_VOC_PRIVATE_DATA` 환경변수로 지정한 **저장소 밖 폴더**를 사용합니다. 티스토리 수집에는 `CHROMEDRIVER_PATH`, 유튜브 검색에는 `YOUTUBE_API_KEY`가 필요합니다.
* 수집 노트북의 출력은 각각 비공개 폴더의 `tistory/`, `youtube/`에 저장됩니다. 수집 후 통합 전에 제품군을 확인해 수동으로 `input/`에 `의류관리기_tistory.csv`, `무선스틱청소기_youtube.csv`처럼 배치해야 합니다. 티스토리의 `url` 열은 통합 코드가 `link`로 바꿉니다. 필요한 열은 `title`, `content`, `date`, `link`(또는 `url`)이며 `platform`은 없으면 출처명으로 채웁니다. 다른 출처의 수집 코드와 원자료는 이 폴더에 포함하지 않았습니다.
* 통합 결과는 같은 비공개 폴더의 `processed/`와 `analysis_input/`에 저장됩니다. 분석 노트북은 `LG_VOC_DATA_DIR`을 `analysis_input/` 경로로 지정해 실행합니다. 필요한 파일은 `의류관리기.csv`, `무선스틱청소기.csv`, `의류관리기_수정.csv`, `무선스틱청소기_수정.csv`입니다.
* 티스토리 글의 게시일이 확인되지 않으면 `date`가 비어 있습니다. 통합 노트북은 게시일 미확인 글과 2022~2024년 밖의 글을 제외합니다. 따라서 검색 결과 건수와 분석 입력 건수는 다를 수 있습니다.
* 분석 노트북의 결과는 실행 위치의 `results/`에 저장됩니다. 이 폴더와 CSV는 `.gitignore`로 공개 대상에서 제외했습니다. 한글 그림 글꼴을 직접 지정할 경우 `LG_VOC_FONT_PATH`를 사용합니다.

## 원본 결과와의 관계

* 300자(공백 포함) 이하 제외는 최종보고서의 기준을 후속 코드로 명시했습니다. 당시의 수작업 제외 내역은 남아 있지 않아 보고서의 최종 건수를 재현한다고 볼 수 없습니다.
* `nva`·`content_nouns` 생성과 분석 입력 CSV 4개는 원본의 Okt 처리 방식을 참고해 구성했습니다. 당시 서로 다른 전처리 버전을 동일하게 재현한 파일이 아닙니다. 기존 보고서 수치·순위와 일치하는지는 확인되지 않았습니다.
* 연관어 계산은 게시글별 단어 경계를 유지하도록 수정했습니다. 공개 노트북을 실행한 값은 당시 보고서의 저장 결과와 별도로 검증해야 합니다.
* 무선청소기 브랜드 분석의 당시 실행본은 보존되지 않았습니다. 공개 노트북으로 포트폴리오의 그림과 같은 결과가 나오는지는 확인되지 않았습니다.
* 게시글 사용 맥락은 실제 사례를 읽고 해석한 결과입니다. 원문과 사례 선별 기록은 이 공개 코드에 포함하지 않았습니다.
