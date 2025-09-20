LB Role
=========

이 롤은 CentOS/RHEL 계열 시스템에서 **HAProxy**를 설치하고 Layer 4 로드밸런서를 구성합니다.  
또한 `firewalld`에 HTTP 서비스를 등록하고, 포트 충돌 방지를 위해 `httpd` 서비스를 중지/비활성화합니다.

요구 사항 (Requirements)
------------------------
```yaml
# 지원 OS 및 요구사항
OS: CentOS 8/9, RHEL 8/9
Ansible: ">=2.14"
Packages:
  - haproxy
  - firewalld
# HAProxy가 분산할 웹 서버 목록
web_backends:
  - { name: "web1", ip: "192.168.10.11", port: 80 }
  - { name: "web2", ip: "192.168.10.14", port: 80 }
Dependencies: []
# 함께 사용 가능
- kangbum01.web   # 웹 서버 롤
- kangbum01.nfs   # NFS 서버 롤
- hosts: lb
  become: true
  roles:
    - role: kangbum01.lb
      vars:
        web_backends:
          - { name: "web1", ip: "192.168.10.11", port: 80 }
          - { name: "web2", ip: "192.168.10.14", port: 80 }
MIT
Author: kangbum01
GitHub: https://github.com/kangbum01
