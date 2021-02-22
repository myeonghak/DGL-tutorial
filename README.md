


DGL 한국어 튜토리얼
==============================================

<center><img src="/asset/dgl_logo.png" align="center" alt="drawing" width="300"/></center>    

<br/>

Deep Graph Library(DGL)은 기존의 DL 프레임워크(e.g. PyTorch, MXNet, Gluon 등)위에 그래프 뉴럴 네트워크 모델을 간편하게 구현하기 위한 `Python` 패키지입니다. DGL은 아키텍쳐 디자인 상에서 [NetworkX](https://networkx.org/)의 API와 패러다임을 따르고 지향하고 있습니다.  


DGL은 그래프 뉴럴넷 구현에서의 Keras로 비유되곤 합니다. 다양한 API 함수들이 제공되고, 다양한 백엔드 프레임워크를 취향에 맞게 사용할 수 있습니다. 해당 튜토리얼에서는, [PyTorch](https://pytorch.org/) 백엔드를 사용한 예제를 제공합니다. 간편하고 직관적인 구현이 DGL의 강점입니다.  

해당 튜토리얼은 [DGL 공식 API 문서](https://docs.dgl.ai/en/latest/new-tutorial/)와 [WWW20](https://github.com/dglai/WWW20-Hands-on-Tutorial), [KDD20](https://github.com/dglai/KDD20-Hands-on-Tutorial)의 내용을 번역, 재구성하여 작성되었으며, DGL 메인 컨트리뷰터 [Minjie Wang](https://github.com/jermainewang)님의 동의와 자문을 구해 만들어 졌음을 밝힙니다.  

공부하는 과정에서 정리하는 목적에서 만든 자료이기 때문에, 부족한 부분이 많습니다.  
잘못된 내용이나 수정이 필요한 부분은 issue나 PR, 메일로 알려주시면 감사하겠습니다!  



----

<br>

Contents
--------

1.	[DGL 기본](/basics/)
2.	[대용량 그래프 데이터 조작하기](/large_graph)


<br>


## 시작하기

해당 튜토리얼은 jupyter notebook으로 작성되어 있습니다. 간편한 환경 셋팅을 위해 docker 컨테이너를 실행하여 jupyter lab 환경에서 실습을 진행합니다.  

### git clone

```
git clone https://github.com/myeonghak/DGL-tutorial.git
cd DGL-tutorial
```

### docker setting  
docker를 사용해 실습 환경을 셋팅합니다.
로컬 환경에서의 셋팅은 [여기](https://docs.dgl.ai/en/0.4.x/install/)를 참고해 주세요.  


**1. 도커 이미지 가져오기**
```
docker pull nilsine11202/dgl-tutorial:1.0
```
<center><img src="/asset/docker_pull.png" align="center" alt="drawing" width="400"/></center>    
image pull이 잘 이루어 졌다면, 아래와 같은 내용을 확인해 볼 수 있습니다.   


```
docker images
```  


<center><img src="/asset/docker_images.png" align="center" alt="drawing" width="600"/></center>    



<br/>



**2. 컨테이너 실행**  

받아온 이미지를 사용해 컨테이너를 실행합니다.  

```
docker run --runtime nvidia -it --name dgl_tuto -p 8885:8885 -v /home:/workspace -d nilsine11202/dgl-tutorial:1.0 /bin/bash

# docker run --runtime nvidia -it --name dgl_tuto --shm-size 128G -p 8885:8885 -v /home:/workspace -d nilsine11202/dgl-tutorial:1.0 /bin/bash
# (large-graph 예제 실행시 Bus error (core dumped) model share memory 에러가 발생할 경우, 위처럼 --shm-size 인자로 도커 컨테이너의 shared memory를 늘림으로써 해결할 수 있습니다)

```
`dgl_tuto`: 컨테이너의 이름으로 사용한 임의의 명칭입니다. 원하시는 이름으로 바꾸어 사용하세요.  
`8885:8885`: jupyter lab 포팅을 위한 포트를 지정해 줍니다. 원하는 포트로 바꾸어 사용할 수 있습니다. 로컬호스트가 사용하지 않을 법한 포트명을 임의로 지정해 주었습니다.  
`/home:/workspace`: docker 컨테이너 내부의 `/home` 디렉터리를 로컬의 `/workspace` 디렉터리로 맵핑해 주었습니다. 역시 원하는 디렉터리로 바꾸어 사용하셔도 됩니다.  

<br/>

**3. 컨테이너로 배시 실행**
```
docker exec -it dgl_tuto bash
```
실행이 성공하면, 컨테이너의 bash에 접근할 수 있습니다.  

<br/>

**4. 주피터 랩 실행하기**
```
jupyter lab --ip=0.0.0.0 --port=8885 --allow-root
```
docker 컨테이너의 배시에서 위의 커맨드를 실행하면, 주피터 환경에 접근할 수 있습니다.  


<br/>


## TO DO  

* custom graph dataset 만들기
* graph visualization
* local 환경 셋팅
* 추천 시스템 예제 적용
