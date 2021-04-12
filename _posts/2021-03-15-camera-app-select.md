---
date: 2021-03-15 21:30
layout: post
title: 안드로이드 카메라앱 선택 강제하기
subtitle:
description:
image: /assets/img/uploads/camera-app-select.png
category: programming
tags:
 - android
author: chanoyoung
---

앱에서 카메라기능을 호출할 경우 위와 같은 화면이 뜨면서 사용할 앱을 선택하게 된다.

이 때 선택 창을 띄우지 않고 강제로 사용앱을 지정하려면 다음과 같이 하면 된다.
```java
Intent intent = new Intent(android.provider.MediaStore.ACTION_IMAGE_CAPTURE);
intent.setPackage("패키지명");
```

기본 카메라앱의 패키지 이름은 제조사마다 다르고, 다음과 같다.

<table>
  <thead>
    <tr>
      <th>제조사</th>
      <th>패키지명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LG</td>
      <td>com.lge.camera</td>
    </tr>
    <tr>
      <td>SAMSUNG</td>
      <td>com.sec.android.app.camera</td>
    </tr>
  </tbody>
</table>


이 때 설치되어 있지 않은 패키지명으로 setPackage를 할 경우 기능 자체가 작동하지 않을 수 있다.  
이를 해결하기 위해 다음과 같이 해당 패키지가 설치되어있는지 확인해볼 수 있다.

```java
public String getPackageName() {
    PackageManager pm = getActivity().getPackageManager();
    LIST<ApplicationInfo> packages = pm.getInstalledApplications(0);

    for (ApplicationInfo packageInfo : packages) {
        String packageName = packageInfo.getPackageName;
        if ("패키지명".equals(packageName)) {
            return packageName
        }
    }
    return "";
}
```

제조사 마다 다른 패키지명을 일일이 찾아서 등록해주어야 하기 때문에 좋은 방법은 아닌 것 같다.

리스트 중에 첫 번째로 나오는게 가장 먼저 깔린 기본앱이 아닐까 생각도 해보았는데 꼭 그런 것은 아닌 것 같다.
