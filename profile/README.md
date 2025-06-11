# Blockchain Based IoT Software Update Platform
> Hansung University Team **Blocker**
<img widht="960" src="https://github.com/user-attachments/assets/1290dadf-f65c-4e51-af90-b5ec2b2ebfa1" />


&nbsp;
## *****Contents*****
- [Project Description](#project-description)
- [Architecture](#architecture)
- [Technologies Used](#technologies-used)
- [Main Features](#-main-features)
  - [Manufacturer](#manufacturer)
  - [Device](#device)
- [Expected Impact](#expected-impact)
- [Achievements and Future Research](#achievements-and-future-research)
- [Additional Info](#additional-info)
- [Team Blocker Developers](#️-team-blocker-developers)


&nbsp;
## *****Project Description*****
본 프로젝트는 IoT 기기의 안전한 소프트웨어 업데이트를 위해 블록체인과 CP-ABE(속성 기반 암호화) 기술을 결합한 분산형 소프트웨어 업데이트 플랫폼이다.   
업데이트 내역을 블록체인에 기록함으로써 제조사가 임의로 수정할 수 없도록 하여 투명성을 확보하고, 스마트 계약을 통해 소프트웨어 배포와 결제를 원자적으로 처리한다.   
CP-ABE를 활용해 제조사의 업데이트 정책과 속성이 일치하는 디바이스만 업데이트가 가능하도록 함으로써 안전한 업데이트를 제공하고, IPFS를 활용해 대용량 업데이트 파일을 분산적으로 저장하여 효율적으로 관리한다.   
이를 통해 기기 인증, 무결성, 감사 가능성, 고가용성을 보장하며, 제조사와 사용자 모두에게 안전하고 효율적인 업데이트 환경을 제공한다.


&nbsp;
## *****Architecture*****
<p align="center">
  <img width="960" alt="architecture-diagram" src="https://github.com/user-attachments/assets/a7cb9ac8-c929-46be-879d-7f68039cad7f" />
</p>


&nbsp;
## *****Technologies Used*****

### Frontend
- React
- Vite
- TypeScript
- JavaScript
- Three.js (시각화 도구)
- Docker

### Backend
- Python
- Flask
- Web3.py (블록체인 연동)
- Docker
- AWS
- Swagger (API 문서화)

### Blockchain
- Solidity (스마트 컨트랙트)
- Ganache (로컬 블록체인 테스트 환경)
- Web3.py
- Docker
- AWS

### Security / Cryptography
- CP-ABE (속성 기반 암호화)
- AES-256 (대칭키 암호화)
- SHA3-256 (무결성 해시)
- ECDSA (전자 서명 및 검증)

### Distributed File System
- IPFS (분산 P2P 파일 시스템)


&nbsp;
## ✨ *****Main Features*****

### Manufacturer
<table>
  <tr>
    <td><img width="500" height="250" src="https://github.com/user-attachments/assets/b9aeac84-ceb9-4d2f-bda7-06174e1e72cd" /></td>
    <td><img width="500" height="250" src="https://github.com/user-attachments/assets/69b90301-c7ef-4aa5-85b9-f2aee1d46f71" /></td>
  </tr>
  <tr>
    <td><img width="500" height="250" src="https://github.com/user-attachments/assets/f9a37c23-d531-4734-a88f-4a39f24d5ed5" /></td>
    <td><img width="500" height="250" src="https://github.com/user-attachments/assets/b1e83948-0e5a-4865-b9f5-79eae5d0b4eb" /></td>
  </tr>
</table>

**제조사 주요 기능**

- **업데이트 파일**을 **AES-256으로 암호화**하고, 생성된 **대칭키(kbj)** 를 **CP-ABE로 암호화**하여 **접근 제어 정책** 적용  
- 암호화된 파일(Es)에 대해 **SHA3-256 해시 값을 생성**하여 **무결성 검증 기준값(hEbj)** 확보  
- 암호화된 파일을 **IPFS에 업로드**하고, 해당 파일의 **콘텐츠 식별자(CID)** 를 획득  
- 업데이트 UID, IPFS 해시(CID), 암호화된 키(encrypted_key)를 **스마트 컨트랙트에 등록**  
- 등록된 데이터를 **ECDSA 개인키로 서명**하고, **서명 결과를 블록체인에 함께 기록**하여 **위변조 방지**  
- **스마트 컨트랙트**를 통해 **소프트웨어 업데이트의 배포 및 결제** 를 **원자적(Atomic)으로 처리**  
- 배포된 **스마트 컨트랙트 주소**를 **레지스트리 컨트랙트에 자동 등록**하여 다른 서비스에서 **중앙 참조** 가능하도록 구성  
- **Three.js**를 활용하여 블록체인 및 IPFS 기반 소프트웨어 업데이트 등록 과정을 시각화
  
&nbsp;
### Device
<table>
  <tr>
    <td><img width="500" height="250" src="https://github.com/user-attachments/assets/1290dadf-f65c-4e51-af90-b5ec2b2ebfa1" /></td>
    <td><img width="500" height="250" src="https://github.com/user-attachments/assets/b0f34620-ff57-46ce-b87a-61108d3c85bc" /></td>
  </tr>
</table>

**디바이스 주요 기능**
- 블록체인에서 **새로운 소프트웨어 업데이트 등록 이벤트를 감지**  
- **IPFS에서 암호화된 업데이트 파일(Es)** 을 다운로드  
- 다운로드된 파일의 **SHA3-256 해시 값을 계산**하고, 등록된 기준 해시(**hEbj**)와 비교하여 **무결성 검증 수행**  
- **CP-ABE로 암호화된 대칭키(encrypted_key)** 를 복호화하여 **원본 대칭키(kbj)** 획득  
- 복호화한 **kbj를 직렬화한 뒤 SHA-256 해싱**하여 **AES-256 키 생성**  
- 생성된 **AES 키를 사용해 업데이트 파일을 복호화**하여 **원본 파일(bj)** 복원  
- 복호화 및 검증이 완료된 파일을 **디바이스에 설치**하고, **설치 완료 여부를 스마트 컨트랙트를 통해 블록체인에 기록**  
- **Three.js**를 활용하여 블록체인 및 IPFS 기반 소프트웨어 업데이트 설치 과정 시각화
- 업데이트 설치 완료 후, 실제 **IoT 기기의 동작(직진, 후진 등)** 을 수행하여 소프트웨어 적용 결과 확인


&nbsp;
## *****Expected Impact*****
1. **보안 위협 차단**  
   IoT 기기의 소프트웨어 업데이트 과정에서 발생할 수 있는 무단 접근, 위조, 결제 미이행 등의 보안 위협을 차단하고  
   기기 인증 및 데이터 무결성을 보장

2. **신뢰성 확보**  
   CP-ABE를 통해 제조사의 정책과 일치하는 속성을 가진 디바이스만 복호화가 가능하며,  
   블록체인 및 스마트 컨트랙트를 통해 결제 및 배포 과정의 신뢰성을 강화

3. **감사 가능성**  
   모든 업데이트 내역이 블록체인에 투명하게 기록되어 조작이 불가능하고, 
   감사 및 컴플라이언스 대응이 용이

4. **확장성 및 고가용성**  
   IPFS 기반의 파일 분산 저장 구조를 통해 대규모 IoT 환경에서도 뛰어난 확장성과 고가용성을 제공

&nbsp;
## *****Achievements and Future Research*****
> ※ **2025년 한국자동차공학회 춘계학술대회** 논문 투고  
> 자동차 ECU 환경의 소프트웨어 업데이트를 위한 해시 함수 성능 평가 연구   
> 속성 만료와 속성 레벨 키 갱신을 활용한 CP-ABE 기반 IoT 소프트웨어 업데이트의 보안성 강화 연구 
>
> ※ **2025 한성대학교 컴퓨터공학부 캡스톤 디자인 우수상** (모바일소프트웨어트랙 부분)
> 
> ※ 추후 SW산학협력프로젝트를 통해 SDV(Software-Defined Vehicle) 환경에 적합한 음성 인식 기반 OTA 소프트웨어 업데이트 적용 기법을 연구할 예정이며, 이를 통해 음성 인식 기능을 도입하여 소프트웨어 업데이트 접근 제어의 보안성을 한층 강화할 계획


&nbsp;
## *****Additional Info*****
| Category       | Description                                |
|----------------|--------------------------------------------|
| Demo Video     | [Watch the demo](https://youtu.be/dioYtYY6i1s) |
| Panel Info     | [View panel](https://github.com/user-attachments/files/20480591/Blocker.pdf) |


&nbsp;
## ⛓️ *****Team Blocker Developers*****
| <a href="https://github.com/kharabiner" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/168187962?v=4" /></a> | <a href="https://github.com/se0y" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/127683099?v=4" /></a> | <a href="https://github.com/3DUCK" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/170965462?v=4" /></a> | <a href="https://github.com/marulog" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/150882419?v=4" /></a> | <a href="https://github.com/mmije0ng" target="_blank"><img width="128" src="https://avatars.githubusercontent.com/u/127730905?v=4" /></a> |
|:-------------:|:------:|:------:|:------:|:------:|
| [박한빈(팀장)](https://github.com/kharabiner) | [공서연](https://github.com/se0y) | [김건우](https://github.com/3DUCK) | [박준희](https://github.com/marulog) | [박미정](https://github.com/mmije0ng) |

### Contact
- **박한빈**: 2271432@hansung.ac.kr  
- **공서연**: 2271014@hansung.ac.kr  
- **김건우**: kermit7520k@gmail.com  
- **박준희**: 1971535@hansung.ac.kr  
- **박미정**: arsvita0116@gmail.com  
