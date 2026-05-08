
# ansible
서버를 코드로 관리하자 = Infrastructure as Code  
똑같은 템플릿을 여러번 실행해도 결과가 달라지지 않는다.(멱등성)  
서버 프로비저닝을 셋팅하여 언제든지 복구 가능하다.  

[RedHat-IaC](https://www.redhat.com/ko/topics/automation/what-is-infrastructure-as-code-iac)  
[RedHat-Ansible](https://www.redhat.com/ko/topics/automation/learning-ansible-tutorial)  

# ansible.cfg
ansible은 ssh를 이용한 에이전트리스다.  
컨트롤 노드의 ansible을 설치하고 메니지드 노드에게 ssh 연결로 코드를 전달한다.  
*`ssh 연결 설정 파일.`*  

# inventory
inventory는 메니지드 노드의 주소를 작성한다.  
*`메니지드 노드 주소 파일.`*  

# playbook.yml
동작 모듈들이 존재한다.  
헤더와 바디로 나뉜다.  
헤더는 메니지드 노드 주소를 지정하고 바디는 행위를 정의한다.  
인벤토리에서 정의된 호스트나 그룹을 지정하여 모듈(행동) 지침을 작성한다.  
*`메니지드 노드 행위 정의 파일`*  

# 변수
inventory의 그룹과 호스트가 사용할 변수를 다음 디렉토리에서 관리한다.  
../group_vars  
../hosts_vars  




# site.yml
playbook.yml의 헤더만 정의한다.  
나머지 모듈 바디는 roles 디렉토리에서 각 서비스마다 정의한다.  
어느 서버든지 같은 모듈로 서비스를 구축할 수 있다.  
단, 변수는 별도  
*`서비스 특화 모듈 헤더`*

# roles/tasks
모든 서비스들의 공통 모듈을 만들어 빠르게 구축할 수 있다.  
playbook.yml의 바디만 정의한다.  
**nginx**는 **nginx-role**을 생성하여 어느 서버에도 적용될 수 있다.  
*`서비스 특화 모듈 바디`*  

# templates
jinja2 문법 {{ 변수 }} 을 사용하며 설정파일을 미리 만들어둔다.  
tasks에 templates를 호출하여 설정파일을 적용한다.  


```
**jinja2 란?**  

*templates/test.txt.j2*  
템플릿 : listen {{ port_number }};  

/ansible/host_vars/host.yml
port_number: 8080

결과 : listen 8080  

매개변수와 값의 변화에 따라 내용이 유동적으로 변하는 파이썬 라이브러리  
엔서블은 파일 내부에 {{ 변수 }} 문법이 존재하면 jinja2로 취급함  
```