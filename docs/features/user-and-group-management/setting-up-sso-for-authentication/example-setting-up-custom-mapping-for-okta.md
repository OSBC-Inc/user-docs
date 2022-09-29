# 예: Okta에 대한 사용자 지정 매핑 설정

다음 페이지에서는 [사용자 지정 매핑 옵션](custom-mapping-option.md)에 사용할 Okta의 역할이라는 사용자 지정 매핑을 구성하는 방법에 대한 2가지 다른 예를 보여줍니다.

### Summary Diagram

![](https://lh5.googleusercontent.com/cuQWU3uMkUSK-SZrKSdwt2V\_vuaJ61bBqpDuTktQWmZ4vNcPsS-jfWsqiMg2lSmGIcPu9MKUJcaYqx4UbImYyWvPbUeqKuU0q4DQRssKnomHovfBnVuPWlwvyaQOrrworlAn\_nMw)

## 구성 1:

이 구성에서:

* Okta 그룹은 Snyk 조직에 매핑됩니다.
* **사용자 프로필은 Okta 그룹이 아닌 각 사용자와 연결됩니다.**

그룹 및 사용자 설정이 완료되면:

1.  **Okta의 Snyk 앱에 속성 추가**

    1.  Directory -> Profile Editor -> Snyk App

        ***

    <img src="https://lh5.googleusercontent.com/h6ww6L16tTWMVhzoVN5Y72oBo51X-WYidqMAO-pTmUksl7akFrgH463S_MMAKDGYdQYzVIYlvN0HCF7tlHMyyIqaQgfdoP9PP6UX7RIJhg-9fFtmLdVwM3tgjVj-h97yKBAS4jGl" alt="" data-size="original">
2. **Add Attribute**\
   ![](https://lh4.googleusercontent.com/R1sr6ZOerCRNxJhGS3ARf0Pebe0dC-tBLP\_80nARDd0LUGTjRY9jA1E-TiTtz4AQvk4aX-pAE\_\_h2S14kgEb6RTSRzZ4O\_1tOcBaCEwpTn2d4HaVuTynjN5D6qE4YSj3LZaiE5WN)
3.  속성 설정

    1. Data Type: 문자열 배열
    2. Display Name: Snyk 조직
    3. Variable Name: snyk\_orgs
    4. Group Priority: 그룹 간에 값 결합
    5. Save and Add Another

    <img src="https://lh3.googleusercontent.com/sIXILVtJJeo9wbjzVSEVNmSVPwkMPeUu1j5yeBxi-mBEgwu4Ejn-4d0tZhtUZay2EV0PkN8wSE0uJgON3csAyXCEKVAAcpShqPKdbz_U1D3ghx5sTCEhBJliRYIIEOf72c3H1TS5" alt="" data-size="original">

    ***
4.  속성 설정

    1. Data Type: 문자열
    2. Display Name: Snyk 사용자 역할
    3. Variable Name: user\_role
    4. Enum: Yes
    5. Scope: User Personal
    6. Attributes Members
       1. Collaborator: collaborator (or collab)
       2. Admin: administrator (or admin)
       3. GroupAdmin: groupadmin
    7. Attribute Required: Yes
    8. Save

    <img src="https://lh3.googleusercontent.com/THGLLKFdDMvTnRrWkoWmC_LGq5GJlw2c9Ht9pLzk_-mUodeDbeFe4xO0F8jDB8Wwvvw-4CloAqFdSubc1VttSbSusmWqw0iju_dhzCuho_3im_uGNf1ShYaakMnT-Bxoizo-L7dB" alt="" data-size="original">

    ***
5. **Directory -> Groups**
   1. 그룹을 선택하고 애플리케이션 탭으로 이동하여 애플리케이션 할당을 클릭하고 Snyk 앱을 그룹에 할당합니다.
   2. Snyk 앱이 있어야 하고 snyk 앱 옆에 있는 연필을 클릭합니다.\
      ![](https://lh3.googleusercontent.com/X3ARoW\_GPcKqIvrowKVPGnBWgziZ4E87hCIRVXzvLkLXOuLvP9fS5y9D-yaCjyWCmr6Co-\_3JSA2ZS-MdM5gEF9JYRi4Ivid-tnijtkpQstm7XgFbhAlnZnRM9D1DKYUsnHm987R)
   3. OKTA 그룹과 연결하려는 Snyk 조직 슬러그를 추가합니다(공백이나 대문자가 없어야 합니다.\
      ![](https://lh5.googleusercontent.com/74SiCm6xOoCRnG9LEpMCeCCHyJA-8viDYL0yNbh0ZQeIpV8wuharGBXp6aIsJB0P1Zjbkn1g2vFr2EcxYawyfh\_axoGISUewc4fXara8oQ4BTsE8\_wlprwd1Df5CeVlYgGgoOjsj)
   4. 해당하는 모든 OKTA 그룹에 대해 1-3단계를 반복하고 필요에 따라 Snyk 조직 슬러그를 수정합니다.
6.  **Directory -> People**

    1. 각 개인에 대해 사용자의 애플리케이션 탭으로 이동하여 앱 옆에 있는 연필을 클릭합니다.\
       ![](https://lh5.googleusercontent.com/7RnhYZ0E24ZoBXe00Zw9jQW\_WbPye2lciWm2qk3zG03mLY6JbsAY7saY-0b26zEGArnDw46MulIgg9XW7Dw9HCt-EODS5qSZquanpNlmfwDHUYL71BQILAfAYifxHf8UBE0BB3Ww)
    2. 올바른 사용자 역할 선택\
       ![](https://lh4.googleusercontent.com/XPclvljK5ZsmLx1Cu3odPCFWz0oj4ZRk9ZkdG-gTto3vMWZWtMQ\_ONHVggh-xHL1UkRwId1eJFh8rZwCrbfUGvhKlL9BBzi3U46d3HXYE8YzFMtS8EIJxBljOim5LvSMarKyNXyZ)

    **구현**

    1. Applications로 이동하여 설정한 Snyk 앱을 클릭합니다.
    2. General Tab -> SAML Settings -> Edit을 클릭하고 다음을 클릭하여 Configure SAML 단계로 이동합니다.
    3. Attribute Statements-> 이름 형식이 **지정되지 않은** 이름 필드로 **역할**을 설정하고 값은 아래 표현식이 됩니다.\
       `appuser.user_role == "groupadmin" ? "snyk-groupadmin" : Arrays.flatten(String.replace(String.replace(String.append("snyk-",String.append(Arrays.toCsvString(appuser.snyk_orgs),"-"+appuser.user_role)),",",",snyk-"),",","-"+appuser.group_user_role+","))`
    4. Next -> Finish을 클릭합니다.

    **역할 표현에 대한 설명:**

    역할이 groupadmin이면 표현식은 다른 모든 것을 무시하고 `snyk-groupadmin`만 전달합니다.

    역할이 groupadmin이 아니면 모든 그룹에 나열된 각 snyk 조직에 대해 표현식이 자동으로 실행됩니다.

    1. 접두사 "`snyk-`"를 snyk 조직 슬러그와 연결
    2. 각 조직 슬러그 끝에 `user_role` 추가

    \
    따라서 최종 결과의 예는 아래와 같습니다.

    \
    예: `"role": [ "snyk-groupadmin", "snyk-customer-facing-tools-admin", "snyk-internal-tools-admin" ]`

## 구성 2:

이 구성에서:

* Okta 그룹은 Snyk 조직에 매핑됩니다.
* Okta 그룹은 Snyk 조직 구성원 역할에 매핑됩니다.
* **Snyk의 사용자 역할은 해당 그룹의 모든 구성원에 대해 각 Okta 그룹에 사전 설정되어 있습니다**.

1. **Okta의 Snyk 앱에 속성 추가**
   1. Directory -> Profile Editor -> Snyk App

![](https://lh5.googleusercontent.com/h6ww6L16tTWMVhzoVN5Y72oBo51X-WYidqMAO-pTmUksl7akFrgH463S\_MMAKDGYdQYzVIYlvN0HCF7tlHMyyIqaQgfdoP9PP6UX7RIJhg-9fFtmLdVwM3tgjVj-h97yKBAS4jGl)

**2. Add Attribute**\
![](https://lh4.googleusercontent.com/R1sr6ZOerCRNxJhGS3ARf0Pebe0dC-tBLP\_80nARDd0LUGTjRY9jA1E-TiTtz4AQvk4aX-pAE\_\_h2S14kgEb6RTSRzZ4O\_1tOcBaCEwpTn2d4HaVuTynjN5D6qE4YSj3LZaiE5WN)

**3. 속성 설정**

1. Data Type: 문자열 배열
2. Display Name: Snyk 조직
3. Variable Name: snyk\_orgs
4. Group Priority: 그룹 간에 값 결합
5. Save and Add Another

![](https://lh3.googleusercontent.com/sIXILVtJJeo9wbjzVSEVNmSVPwkMPeUu1j5yeBxi-mBEgwu4Ejn-4d0tZhtUZay2EV0PkN8wSE0uJgON3csAyXCEKVAAcpShqPKdbz\_U1D3ghx5sTCEhBJliRYIIEOf72c3H1TS5)\
\
**4. Directory -> Groups**

1. 그룹을 선택하고 애플리케이션 탭으로 이동하여 애플리케이션 할당을 클릭하고 Snyk 앱을 그룹에 할당합니다.
2. Snyk 앱이 있어야 하고 snyk 앱 옆에 있는 연필을 클릭합니다.\
   ![](https://lh3.googleusercontent.com/X3ARoW\_GPcKqIvrowKVPGnBWgziZ4E87hCIRVXzvLkLXOuLvP9fS5y9D-yaCjyWCmr6Co-\_3JSA2ZS-MdM5gEF9JYRi4Ivid-tnijtkpQstm7XgFbhAlnZnRM9D1DKYUsnHm987R)
3. OKTA 그룹과 연결하려는 Snyk 조직 슬러그를 추가합니다(공백이나 대문자가 없어야 함 \
   **NOTE**: 이 구성에서는 이 Snyk 조직 슬러그 할당 내에 역할을 추가합니다.\
   \
   ![](https://lh4.googleusercontent.com/qUN0SI64WQqAGCs2YPrvIW0lyZAyZDnGgpYe\_mXyGIPa2XqgBJJa3DBpg\_qGdoHxXql7kNrzrBkzY7T660es0qGcSH5wSbBw1DANk9f1\_q6SHDQXjxNFKRaVVCuZICVkFbnGYUz6)
4. 적용 가능한 모든 OKTA 그룹에 대해 1-3단계를 반복합니다. 이렇게 하면 구성된 그룹 내의 각 사용자에게 동일한 orgslug와 역할이 모두 할당됩니다.

### 구현

1. Applications로 이동하여 설정한 Snyk 앱을 클릭합니다.
2. General Tab -> SAML Settings -> Edit을 클릭하고 다음을 클릭하여 Configure SAML 단계로 이동합니다.
3. 지정되지 않은 유형의 "role"이라는 속성 문 설정
4.  Attribute Statements-> 이름 형식이 **지정되지 않은** 이름 필드로 **역할**을 설정하고 값은 아래 표현식이 됩니다.

    `Arrays.flatten(String.replace(String.append("snyk-",Arrays.toCsvString(appuser.snyk_orgs)),",",",snyk-"))`

### 값 표현의 설명

1.  최종 결과는 아래와 같아야 합니다. **role** 속성의 표현식은 snyk\_orgs 값(- **OR** 포함) 앞에 'snyk'을 자동으로 추가하여 최종 결과가 아래 예와 유사하게 보일 것입니다.\\

    예시 결과: `[“snyk-org1-admin”,”snyk-org2-admin”, “snyk-org3-collaborator”,”snyk-org4-collaborator”,”snyk-groupadmin”]`
