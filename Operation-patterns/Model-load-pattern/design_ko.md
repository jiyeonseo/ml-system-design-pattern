# Model load pattern

## Usecase
- 서버 이미지 업데이트보다 모델 업데이트가 더 잦은 경우. 
- 서버 이미지를 여러 모델에 재사용하려는 경우.

## Architecture
클라우드 플랫폼이나 컨테이너를 이용한 서비스 운영은 이미 일반적이지만, 여전히 ML 모델을 서버 이미지로 관리하고 버전 관리하는 것은 중요한 고려 사항입니다. 빌드 서버 혹은 컨테이너 이미지를 모델 파일과 별도로 사용하고 관리도 따로 할 수 있습니다. model-load pattern은 서버 이미지와 모델 파일을 별도로 작성하고 따로 실행함으로써 서버 이미지를 경량화할 수 있는 패턴입니다. 또, 서버 이미지의 범용성을 높여 동일 이미지로 여러 추론 모델에 재사용할 수 있습니다. 이 패턴은 모델들이 동일한 서버 이미지에 의존적일 때 유용합니다.<br> 
 이 패턴에서 서비스를 릴리즈하려면, 먼저 예측 서버를 플랫폼에 배포한 다음, 프로세스의 시작으로 이미지 파일을 다운로드합니다. 서버에서 실행될 모델을 유연하게 구성을 위해 환경 변수를 이용할 수도 있습니다.<br> 
 이 패턴의 단점은 모델이 라이브러리 버전에 의존적인 경우, 모델이 사용하는 라이브러리 버전과 이미지에 설치된 라이브러리 버전을 동일하게 관리해 주어야 한다는 것입니다. 서버 이미지와 모델 파일이 늘어나고 복잡해짐에 따라 운영 부하가 증가할 수 있습니다

## Diagram
![diagram](diagram.png)


## Pros
- 모델과 서버 이미지의 버전 구분. 
- 서버 이미지 재사용. 
- 서버 이미지 경량화. 

## Cons
- 서비스를 시작하는데 오래걸릴 수 있습니다. (서버와 모델 파일 로드가 차례로 진행되기 때문에)
-  이미지와 모델 지원 버전 관리.

## Needs consideration
- 서버 이미지와 모델 파일의 버전 및 의존성 관리.