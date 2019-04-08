---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: user access, Cloud IAM roles, encryption keys

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 사용자 액세스 관리
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}는 암호화 키에 대한 액세스 및 사용자 관리에 도움이 되도록 {{site.data.keyword.iamlong}}에서 관리하는 중앙 집중식 액세스 제어 시스템을 지원합니다.
{: shortdesc}

새 사용자를 자신의 계정이나 서비스에 초대할 때 액세스 권한을 부여하는 것이 좋습니다. 예를 들어, 다음 가이드라인을 고려하십시오.

- **Cloud IAM 역할을 지정하여 계정에서 리소스에 대한 사용자 액세스를 사용합니다.**
    관리자 인증 정보를 공유하는 대신에 계정의 암호화 키에 액세스해야 하는 사용자를 위한 새 정책을 작성합니다. 계정의 관리자인 경우에는 계정의 모든 리소스에 대한 액세스 권한과 함께 _관리자_ 정책이 자동 지정됩니다.
- **필요한 최소 범위에서 역할 및 권한을 부여합니다. **
    예를 들어, 사용자가 지정된 영역 내에서 키의 상위 레벨 보기에만 액세스해야 하는 경우 사용자에게 해당 영역에 대한 _독자_ 역할을 부여합니다.
- **액세스 제어를 관리하고 키 리소스를 삭제할 수 있는 대상에 대해 주기적으로 감사를 실시합니다.**
    사용자에게 _관리자_ 역할을 부여한다는 것은 사용자가 리소스를 영구 삭제할 수 있음은 물론 다른 사용자에 대한 서비스 정책을 수정할 수도 있음을 의미합니다.

## 역할 및 권한
{: #roles}

IAM({{site.data.keyword.iamshort}})을 사용하면 계정에서 사용자 및 리소스에 대한 액세스를 관리하고 정의할 수 있습니다.

액세스를 간소화하기 위해 {{site.data.keyword.hscrypto}}는 사용자가 지정된 역할에 따라 각 사용자가 서비스에 대한 서로 다른 보기를 가질 수 있도록 Cloud IAM 역할에 맞게 조정합니다. 서비스에 대한 보안 관리자인 경우 팀의 구성원에게 부여할 특정 {{site.data.keyword.hscrypto}} 권한에 대응되는 Cloud IAM 역할을 지정할 수 있습니다.

다음 표에서는 ID 및 액세스 역할이 {{site.data.keyword.hscrypto}} 권한에 맵핑되는 방법을 보여줍니다.
<table>
  <tr>
    <th>서비스 액세스 역할</th>
    <th>설명</th>
    <th>조치</th>
  </tr>
  <tr>
    <td><p>독자</p></td>
    <td><p>독자는 키에 대한 상위 레벨 보기를 찾아보고 랩핑 및 랩핑 해제 조치를 수행할 수 있습니다. 독자는 키 자료에 액세스하거나 이를 수정할 수 없습니다.</p></td>
    <td>
      <p>
        <ul>
          <li>키 보기</li>
          <li>키 랩핑</li>
          <li>키 랩핑 해제</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>작성자</p></td>
    <td><p>작성자는 키를 작성하고 키를 수정하며 키 자료에 액세스할 수 있습니다.</p></td>
    <td>
      <p>
        <ul>
          <li>키 작성</li>
          <li>키 보기</li>
          <li>키 랩핑</li>
          <li>키 랩핑 해제</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>관리자</p></td>
    <td><p>관리자는 키 삭제, 새 사용자 초대 및 다른 사용자를 위한 액세스 정책 지정 기능을 포함하여 독자와 작성자가 수행할 수 있는 모든 조치를 수행할 수 있습니다.</p></td>
    <td>
      <p>
        <ul>
          <li>독자 또는 작성자가 수행할 수 있는 모든 조치</li>
          <li>키 삭제</li>
          <li>액세스 정책 지정</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">표 1. ID 및 액세스 역할이 {{site.data.keyword.hscrypto}} 권한에 맵핑되는 방법에 대한 설명</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

{{site.data.keyword.iamshort}}에 대해 자세히 알아보려면 [사용자 역할 및 권한](/docs/iam/users_roles.html#userroles)을 확인하십시오.

### 다음에 수행할 작업
{: #manage-access-next}

계정 소유자와 관리자는 사용자를 초대할 수 있으며 사용자가 수행할 수 있는 {{site.data.keyword.hscrypto}} 조치에 대응되는 서비스 정책을 설정할 수 있습니다.

- {{site.data.keyword.cloud_notm}} UI에서 사용자 역할을 지정하는 방법에 대한 자세한 정보는 [IAM 액세스 관리](/docs/iam/mngiam.html)를 참조하십시오.
- 특정 암호화 키에 액세스하기 위한 고급 권한 부여에 대해 알아보려면 [키에 대한 액세스 관리](/docs/services/hs-crypto/manage-access-api.html)를 참조하십시오.
