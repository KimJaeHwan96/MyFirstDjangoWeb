참고자료: 파이썬 웹프로그래밍 기본편, 실전편 (김석훈)   
언어: python   
웹 프레임워크: Django   
웹 호스팅 서비스: pythonanywhere      
Paas로 배포하는 것은 처음이고 배포자체는 [클린코드를 위한 테스트 주도 개발(해리 J.W. 퍼시벌)](https://github.com/KimJaeHwan96/TDDforCleanCode)에서 Iaas로 배포하는 것에 이어 2번째입니다.    

- - -


# 11 Deploy
## 11.1 클라우드 컴퓨팅
서버를 구매할때 AWS, Azure, DigitalOcean과 같은 Iaas(Infrastructure as a service)와 pythonanywhere, heroku와 같은 Paas(platform as a service)가 구분 됩니다.   

초보자들이나 배포가 목적인사람은 paas로 배포하는 게 스트레스도 덜받고 좋지만 공부하는 입장에서는 Iaas로 배포해보는 것이 좋다고 생각되어집니다.    

저는 paas로 한번도 배포를 해보지 않았기 때문에 무료 서버를 제공하는 pythonanywhere를 사용하여 배포하였습니다.    

pythonanywhere를 사용하는 방법은 구글링할때 많이 봐왔기 때문에 여기에 따로 적진 않았습니다.   
  
pythonanywhere는 서버에 개발한 프로젝트를 복사할때 git clone으로 github에 올린 코드를 다운받을수도 있지만 프로젝트를 압축하여 .zip파일을 업로드하고 unzip .zip 명령으로 코드를 복사할수 있는 편리함이 있습니다.   

무료 서버를 이용하시면 제가 배포한 사이트처럼 id.pythonanywhere.com으로 도메인이 고정됩니다. 그렇기 때문에 자기가 원하는 도메인을 취득하고 배포하고 싶을때는 유료 서버를 사용하는 것이 좋습니다.  

http://kjh96.pythonanywhere.com   


<img src="https://user-images.githubusercontent.com/64777061/95173599-d7914000-07f3-11eb-9892-a00aafb4050b.PNG" width="50%" height="60%"></img>


## 11.2 배포 시 중요한 sercet_key 관리
Django에는 secret_key가 존재하는데 이 키는 프로젝트 내에서 암호화가 필요할 때 사용되는 항목으로 외부에 노출되어서는 안됩니다.   

Two Scoops of Django의 51p에서는 이러한 sercet_key를 하드코딩하는 것을 방지하는 방법 중 하나로 json파일을 이용할 것을 권합니다   


    with open("secrets.json") as f:
        secrets = json.loads(f.read())
    def get_secret(setting, secrets=secrets):
      """비밀 변수를 가져오거나 명시적 예외를 반환한다"""
      try:
          return secrets[setting]
      except KeyError:
          error_msg = "Set the {0} environment variable".format(setting)
          raise
    SECRET_KEY = get_secret("SECRET_KEY")
    
    
sercets.json 파일을 만들어 키 값을 저장합니다.   
그 키 값을 settings.py에 읽어 secret_key에 저장하는 방법입니다.

