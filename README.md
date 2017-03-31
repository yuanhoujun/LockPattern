# LockPattern 
>original by Sym [LockPattern](https://github.com/sym900728/LockPattern)

## Description

>Imitate Alipay gesture password

>自定义手势密码解锁

## Starting

>创建手势密码可以查看 CreateGestureActivity.java 文件.  
>登陆验证手势密码可以看 GestureLoginActivity.java 文件.

## Features

![设置密码](http://i.imgur.com/1Wv0LpM.gif)

* 使用了 JakeWharton/butterknife [butterknife](https://github.com/JakeWharton/butterknife)

* 使用了 ACache 来存储手势密码

```java
private void saveChosenPattern(List<LockPatternView.Cell> cells) {
    byte[] bytes = LockPatternUtil.patternToHash(cells);
    aCache.put(Constant.GESTURE_PASSWORD, bytes);
}
```

**Warning**: 使用 ACache 类保存密码并不是无限期的. 具体期限可以查看 ACache 类.

* 使用了 SHA 算法保存手势密码

```java
public static byte[] patternToHash(List<LockPatternView.Cell> pattern) {
    if (pattern == null) {
        return null;
    } else {
        int size = pattern.size();
        byte[] res = new byte[size];
        for (int i = 0; i < size; i++) {
            LockPatternView.Cell cell = pattern.get(i);
            res[i] = (byte) cell.getIndex();
        }
        MessageDigest md = null;
        try {
            md = MessageDigest.getInstance("SHA-1");
            return md.digest(res);
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
            return res;
        }
    }
}
```

* 可以开启震动模式，当选中一个圈的时候，手机会震动

```java
public void setTactileFeedbackEnabled(boolean tactileFeedbackEnabled) {
	mEnableHapticFeedback = tactileFeedbackEnabled;
}
```

* 开启绘制路径隐藏模式

 ![默认显示](http://i.imgur.com/LFbhE8W.gif)

```java
public void setInStealthMode(boolean inStealthMode) {
	mInStealthMode = inStealthMode;
}
```

* 可以开启绘制点隐藏模式

![仅隐藏点](http://i.imgur.com/rKWUHsE.gif)

```java
	public void setStealthPoint(boolean stealthPoint) {
			mStealthPoint = stealthPoint;
		}
	or
	app:stealth_point="true"
```
* 自定义属性
***
属性都提供各自的get和set方法

| LockPatternView 属性名      |    类型 |
| :-------- | --------:|
| stealth_point    | boolean |
| default_color    |   int   |
| selector_color   |   int   |
| error_color      |   int   |

***
| LockPatternIndicator 属性名 |    类型 |
| :-------- | --------:|
| idc_default_color    | boolean |
| idc_default_color    |   int   |
| idc_selector_color   |   int   |

## Contact

如果你有什么问题, 或者什么建议, 可以发邮件给我.  
Email address: wizong@126.com

## LICENSE

    Copyright 2016 wizong

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.