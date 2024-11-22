
# 프론트엔드 배포 파이프라인

![프론트엔드 파이프라인 사진](https://raw.githubusercontent.com/sanghyuk-2i/voyage-test/refs/heads/docs/docs/deployment-pipline.png)

## 개요


GitHub Actions에 워크플로우를 작성해 다음과 같이 배포가 진행되도록 합니다.

1. 저장소를 체크아웃합니다.
2. Node.js 18.x 버전을 설정합니다.
3. 프로젝트 의존성을 설치합니다.
4. Next.js 프로젝트를 빌드합니다.
5. AWS 자격 증명을 구성합니다.
6. 빌드된 파일을 S3 버킷에 동기화합니다.
7. CloudFront 캐시를 무효화합니다.

## 주요 링크

- S3 버킷 웹사이트 엔드포인트: http://voyage-practice.s3-website.ap-northeast-2.amazonaws.com
- CloudFrount 배포 도메인 이름: https://d3rk1mcxi48sul.cloudfront.net

## 주요 개념

- GitHub Actions과 CI/CD 도구: 
  <br />
  **CI/CD**는 코드 변경을 자동으로 테스트하고, 배포까지 이어지게 해주는 자동화 시스템이며 CI는 팀원들의 코드를 자주 합치고 문제를 빨리 찾게 도와주고, CD는 잘 통합된 코드를 서버에 자동으로 올려줍니다.
  **GitHub Actions**는 GitHub에서 코드 변경이 일어날 때 빌드, 테스트, 배포 같은 CI/CD 작업을 자동으로 해주는 도구입니다. YAML 파일로 워크플로를 설정해서, 코드 푸시나 PR이 생기면 바로 실행되도록 만들 수 있습니다.
- S3와 스토리지:
  <br />
  **S3**는 AWS에서 제공하는 파일 저장 공간으로, 사진이나 문서 같은 파일을 저장하고 필요할 때 불러올 수 있습니다. 스토리지는 데이터를 저장하는 곳인데, S3는 파일 단위로 관리하는 객체 스토리지라고 합니다.
- CloudFront와 CDN: 
  <br />
  **CloudFront**는 AWS에서 제공하는 CDN(Content Delivery Network) 서비스로, 전 세계 서버에 콘텐츠를 캐싱해 사용자와 가까운 서버에서 데이터를 전달합니다. CDN은 사용자가 요청하면 가장 가까운 엣지 서버에서 콘텐츠를 제공하므로 로딩 속도가 빨라지고, 원본 서버의 트래픽 부담도 줄여줍니다. 
  보통은 정적 파일(이미지, 동영상) 위주로 저장하고 관리합니다.
- 캐시 무효화(Cache Invalidation):
  <br />
  **캐시 무효화**는 업데이트된 콘텐츠를 사용자가 빠르게 볼 수 있도록 기존 캐시된 파일을 강제로 삭제하는 작업입니다. 일반적으로 파일이 수정되면 CDN 서버에 여전히 오래된 파일이 남아있기 때문에 캐시를 무효화해야 하며 CloudFront에서도 “Invalidation”을 사용해 특정 파일이나 전체 캐시를 갱신할 수 있습니다. 
- Repository secret과 환경변수:
  <br />
  **환경변수**는 애플리케이션 실행에 필요한 설정값(예: API 키, DB URL)을 외부에서 관리해 보안을 지켜줄 수 있습니다. 코드에 민감한 값을 직접 넣지 않고, 실행 환경에 따라 다르게 설정할 수 있습니다. GitHub의 Repository Secrets에 환경변수를 안전하게 저장하고, Github Action 워크플로에서 사용할 수 있습니다.
