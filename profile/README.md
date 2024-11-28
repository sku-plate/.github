# 🍕 SKUPLATE
프로젝트 기간 : 2023. 09. 27 ~ 2023. 11. 21

"망고플레이터"의 서비스 종료를 앞두고, 이를 대체하는 대학가 맛집 공유 웹앱 프로젝트입니다.

<br/><br/>

<div dir="auto">
  <div class="markdown-heading" dir="auto">
    <h2 class="heading-element" dir="auto"> 멋쟁이사자처럼 대학 동아리 11기 - SKUPLATE 팀 </h2>
  </div>
  <markdown-accessiblity-table data-catalyst="">
    <table>
      <thead>
        <tr>
          <th><a href="https://github.com/taehwan01"><img src="https://github.com/taehwan01.png" width="100px" style="max-width: 100%;"><br>김태환 [FrontEnd & BackEnd]</a></th>
          <th><a href="https://github.com/TirTir"><img src="https://github.com/TirTir.png" width="100px" style="max-width: 100%;"><br>김유진 [FrontEnd]</a></th>
        </tr>
      </thead>
    </table>
</markdown-accessiblity-table>
</div>

<br/><br/>

## SKUPLATE Repository
- [SKUPLATE React - FrontEnd](https://github.com/sku-plate/sku-plate-react)
- [SKUPLATE Express - BackEnd](https://github.com/sku-plate/sku-plate-express)

<br/><br/>

## SKUPLATE Main Page 화면
<div align="center">
  <img alt="SKUPLATE_WEB_VIEW" src="https://github.com/user-attachments/assets/18eeffac-b1f6-403c-914e-5fcacca5dbde" width="300px" max-width="38%">
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <img alt="SKUPLATE_APP_VIEW" src="https://github.com/user-attachments/assets/0a2f1f68-1fb4-474d-80c7-6a5ce0d8a813" width="300px" max-width="38%">
</div>

<br/><br/>

## 주요 기능
- **회원 관리**
  
  카카오 기반 OAuth를 활용하여 회원 관리

- **식당 관리**
  
  식당 태그 / 카테고리 별 목록 조회
  
  식당 상세 조회(메뉴, 카카오맵, 식당 연락처 등)
  
  식당 정보 관리
  
  식당 스크랩하여 마이페이지에서 조회하기
  
  식당 리뷰 등록하기

<br/><br/>

## 개발 환경
### 개발 도구
<img src="https://img.shields.io/badge/VS%20Code-000000?style=for-the-badge&logo=&logoColor=white">

### Language
<img src="https://img.shields.io/badge/JavaScript-000000?style=for-the-badge&logo=javascript&logoColor=F7DF1E">

### BackEnd
<p>
  <img src="https://img.shields.io/badge/Node.js-000000?style=for-the-badge&logo=nodedotjs&logoColor=5fa04e">
  <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=ffffff">
</p>

### FrontEnd
<img src="https://img.shields.io/badge/React-000000?style=for-the-badge&logo=react&logoColor=61DAFB">

### Database
<img src="https://img.shields.io/badge/MongoDB-000000?style=for-the-badge&logo=mongodb&logoColor=47a248">

### Deployment
<p>
  <img src="https://img.shields.io/badge/AWS%20EC2-000000?style=for-the-badge&logo=amazonec2&logoColor=FF9900">
  <img src="https://img.shields.io/badge/AWS%20S3-000000?style=for-the-badge&logo=amazons3&logoColor=569A31">
  <img src="https://img.shields.io/badge/AWS%20Route53-000000?style=for-the-badge&logo=amazonroute53&logoColor=8c4fff">
</p>

### Others
<p>
  <img src="https://img.shields.io/badge/Figma-000000?style=for-the-badge&logo=figma&logoColor=#F24E1E">
  <img src="https://img.shields.io/badge/Notion-000000?style=for-the-badge&logo=notion&logoColor=ffffff">
</p>

<br/><br/>

## 시스템 아키텍처
<img alt="SKUPLATE_SYSTEM_ARCHITECTURE" src="https://github.com/user-attachments/assets/94766fc3-6790-4d3d-a095-d224f0fcfb08" width="100%">


<br/><br/>

## 데이터 구조 및 스키마 설계
해당 프로젝트에서는 MongoDB를 사용하여 데이터를 저장하고, Mongoose를 통해 데이터 모델을 정의했습니다.

### User 스키마
| 필드명               | 타입           | 설명                                               | 필수 여부      | 기본값          |
|-------------------|--------------|------------------------------------------------|------------|---------------|
| `name`           | `String`     | 사용자 이름                                       | ✅         | 없음            |
| `profileImage`    | `String`     | 프로필 이미지 경로                                 | ❌         | `default.jpg` |
| `email`          | `String`     | 사용자 이메일 (고유값)                              | ❌         | 없음            |
| `bookmarkedRestaurants` | `ObjectId[]` | 즐겨찾기한 식당 목록 (Restaurant 참조)            | ❌         | 없음            |
| `active`         | `Boolean`    | 활성 상태 여부 (비활성 사용자는 제외)                | ❌         | `true`         |

### 가상 필드 (Virtual Field)
- `bookmarks`: `bookmarkedRestaurants` 필드와 `Restaurant` 컬렉션의 관계를 참조합니다.

### 미들웨어
- 쿼리 미들웨어: 모든 `find` 쿼리에서 `active`가 `false`인 사용자는 자동으로 제외됩니다.

```javascript
userSchema.pre(/^find/, function (next) {
  this.find({ active: { $ne: false } });
  next();
});
```

<br/>

### Restaurant 스키마
| 필드명       | 타입          | 설명                                | 필수 여부      | 기본값    |
|------------|-------------|-----------------------------------|------------|---------|
| `name`     | `String`    | 식당 이름 (고유값)                     | ✅         | 없음      |
| `typeOfFood` | `String`    | 음식 종류                             | ✅         | 없음      |
| `address`  | `String`    | 주소                                | ✅         | 없음      |
| `menu`     | `Array`     | 메뉴 목록 (`name`, `price` 필드 포함) | ❌         | 없음      |
| `images`   | `String[]`  | 식당 이미지 경로 배열                     | ❌         | 없음      |
| `tags`     | `String[]`  | 식당 태그                             | ❌         | 없음      |
| `active`   | `Boolean`   | 활성 상태 여부                         | ❌         | `true`  |

### 가상 필드 (Virtual Field)
- `reviews`: `Restaurant`과 `Review` 컬렉션의 관계를 참조합니다.

<br/>

### Review 스키마
| 필드명        | 타입          | 설명                           | 필수 여부      | 기본값            |
|-------------|-------------|----------------------------|------------|----------------|
| `restaurant` | `ObjectId`  | 리뷰 대상 식당 (Restaurant 참조)    | ✅         | 없음             |
| `user`       | `ObjectId`  | 리뷰 작성자 (User 참조)           | ✅         | 없음             |
| `content`    | `String`    | 리뷰 내용                        | ✅         | 없음             |
| `rating`     | `Number`    | 평점                           | ✅         | 없음             |
| `createdAt`  | `Date`      | 리뷰 작성 시간                    | ❌         | 현재 시간 (`Date.now`) |

### 미들웨어

- 쿼리 미들웨어: `find` 쿼리 실행 시 `user` 필드의 `name`만 자동으로 포함되도록 설정됩니다.

```javascript
reviewSchema.pre(/^find/, function (next) {
  this.populate({
    path: 'user',
    select: 'name',
  });
  next();
});
```

<br/>

### 컬렉션 간 관계

1. **User ↔ Restaurant**
   - 사용자는 즐겨찾기한 식당 목록을 관리 (`bookmarkedRestaurants`)합니다.
   - `bookmarks` 가상 필드를 통해 `Restaurant`와의 관계를 참조합니다.

2. **Restaurant ↔ Review**
   - 식당은 리뷰 목록 (`reviews`)을 가집니다.
   - `reviews` 가상 필드를 통해 `Review`와의 관계를 참조합니다.

3. **Review ↔ User**
   - 리뷰 작성자는 `user` 필드를 통해 `User`를 참조합니다.
