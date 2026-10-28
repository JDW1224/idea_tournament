# 얼굴 인식과 인증 장치 실험

OpenCV·dlib로 얼굴 등록, 특징 추출, 웹캠 인식을 수행하는 Python 프로젝트다. Arduino 지문 센서·키패드·서보와 Python OTP 예제도 함께 보관한다.

이 저장소는 [smilejw12/OpenCv-project](https://github.com/smilejw12/OpenCv-project)의 **포크**다. 기존 소개인 `2021 cbnu contest`와 원본 출처를 유지하며, 아래 내용은 저장된 코드의 기능을 설명한다.

## 주요 기능

- 웹캠 얼굴 등록: `n`으로 사람별 폴더 생성, `s`로 이미지 저장, `q`로 종료.
- dlib 모델로 128차원 얼굴 특징을 추출하고 사람별 평균을 CSV로 저장.
- 등록한 특징과 웹캠 얼굴을 비교하고 중심점 추적으로 프레임 간 인식 결과 연결.
- 별도 하드웨어 예제: 지문 인식 결과에 따른 서보 동작, 키패드 입력, 시리얼 통신과 OTP 비교.

## 구성

| 파일 | 역할 |
| --- | --- |
| `get_faces_from_camera.py` | 얼굴 이미지 수집 |
| `features_extraction_to_csv.py` | 특징 추출 및 `data/features_all.csv` 생성 |
| `face_reco_from_camera_ot_multi_people.py` | 웹캠 얼굴 인식·추적 |
| `data/data_dlib/` | dlib 모델 파일 |
| `motor_finger.zip` | 지문 센서·서보 Arduino 스케치 |
| `real_final_otp_keypad.zip` | 키패드·서보 스케치 및 Python OTP 실험 |

## 준비 및 실행

얼굴 인식 코드는 Python, dlib, NumPy, OpenCV, pandas와 웹캠을 사용한다. 기존 README의 환경 목록에는 scikit-image도 포함되어 있다. Python·라이브러리 버전은 고정되어 있지 않다.

`data/data_dlib/`에 다음 두 모델이 필요하다.

- `dlib_face_recognition_resnet_model_v1.dat`: 저장소에 포함.
- `shape_predictor_68_face_landmarks.dat`: 별도 준비. [기존 README에서 안내한 파일](https://github.com/italojs/facial-landmarks-recognition/blob/master/shape_predictor_68_face_landmarks.dat)을 같은 폴더에 배치한다.

저장소 루트에서 순서대로 실행한다.

```bash
python get_faces_from_camera.py
python features_extraction_to_csv.py
python face_reco_from_camera_ot_multi_people.py
```

얼굴 이미지는 `data/data_faces_from_camera/`에 저장된다. 기본 카메라 인덱스는 `0`이다. 수집 명령은 기존 README의 오기를 실제 파일명에 맞췄다.

하드웨어 예제에는 Arduino 환경과 Adafruit Fingerprint·Servo·Keypad 라이브러리, Python의 pyserial·pyotp가 필요하다. 보드, 배선과 시리얼 포트는 각 예제에 맞춰 설정한다. 얼굴 인식 코드와 하드웨어 예제가 하나의 인증 흐름으로 연결되어 있지는 않다.

OTP 예제는 실행 전에 환경변수 `OTP_SECRET`에 시드를 설정한다. 선택 변수 `OTP_ACCOUNT_NAME`, `OTP_ISSUER`로 등록용 계정 이름과 발급자 표기를 지정할 수 있다. 이 값은 공개 저장소에 넣지 않는다.

## 실행 범위

모델·카메라·하드웨어 환경에서 이번에 재실행하지 않았다. 실제 얼굴 이미지·특징 데이터는 공개 저장소에 추가하지 않는다.

## 원본 및 참고 자료

- 원본 저장소: [smilejw12/OpenCv-project](https://github.com/smilejw12/OpenCv-project)
- 기존 README의 참고 글: [AdaminXie의 얼굴 인식 글](https://www.cnblogs.com/AdaminXie/p/9010298.html)

원본 코드의 저작자 표기를 유지한다. 저장소에는 별도 LICENSE 파일이 없으며 새 라이선스를 추가하지 않았다.
