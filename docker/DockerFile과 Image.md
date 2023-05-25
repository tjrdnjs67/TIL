-  DockerFile을 통해 Image를 생성한다.
-  Image를 통해서 Docker Container를 생성할 수 있다.
- 기존의 소스코드가 변경되었다면 DockerFile을 통해서 Image를 새로 생성해고 새로 생성된 Image를 통해서 Container를 새로 생성해야 변경된 코드가 적용된다.
- Docker의 **일관성** 과 **재현성** 
	- Dockerfile에 명시된 명령어를 사용해 만든 Docker Image는 항상 동일한 결과를 제공한다. 
	- 동일한 Dockerfile을 사용해 다른 환경에서 이미지를 생성하더라도, 그 결과는 원본과 동일하게 나타난다.(서로 다른 환경에서 동일한 애플리케이션 동작을 보장)
```
docker build .

```

### Image는 Read-Only

![Alt text](docker_img1.png)

### Image Layer 구조
- **배경** 
	1. Docker의 Image는 컨테이너를 만드는 압축파일로 생각하면 편하다.
	2. Docker Image는 Container를 만들기 위한 모든 정보를 가지고 있다.
	3. Image는 다시 빌드하지 않는 한 코드를 변경할 수 없다.
	4. Docker Image는 컨테이너를 실행하기 위한 모든 정보를 가지고 있기 때문에 보통 용량이 수백MB이다.
	5. Image 불변성 때문에 수정사항이 발생하면 파일이 단 하나 추가된 Image를 새로 다운받아야 하는데 수백MB를 다시 다운 받는 것은 매우 비효율적이다.
	6. Docker는 이러한 문제를 해결하기 위해 Layer라는 개념을 사용한다.

![Alt text](docker_img2.png)
**이렇게 여러 이미지가 레이어를 공유할 수 있기 때문에 파일 시스템에서 차지하는 전체 용량이 감소한다.**

![Alt text](docker_img3.png)
둘 다 109MB를 사용한다고 나왔지만 중복된 Layer 용량을 빼면 실제로 사용되는 용량은 훨씬 작다.