# 虚幻运行时单例系统
---
### 1.简介

只需继承USingletonBase即可实现该类的单例模式，C++和蓝图都可使用，提供全局访问函数，该单例实例与UGameInstance共享生命周期。
### 2.在C++中使用
### 2.1在C++中创建单例类，见UCppSingletonExample示例
```C++
// Copyright 2021 (C) Li Zi Jun.

#pragma once

#include "CoreMinimal.h"
#include "UObject/NoExportTypes.h"
#include "SingletonBase.h"
#include "CppSingletonExample.generated.h"

/**
 * Cpp Singleton Example
 * Simply inherited from USingletonBase, at the beginning of the game will be according to the need to instantiate the singleton object
 */
UCLASS()
class UCppSingletonExample : public USingletonBase
{
	GENERATED_BODY()
public:
	/** Does the thing. */
	UFUNCTION(BlueprintCallable, Category = "CppSingleton")
		FString GetNowTime();

	/** Does the thing. */
	UFUNCTION(BlueprintCallable, Category = "CppSingleton")
		FString DateTimeToString(FDateTime Time);

protected:
	bool GetAutoInstantiate() const override;

	void Initialize_Implementation() override;

	void BeginPlay_Implementation() override;

	void Tick_Implementation(float DeltaTime) override;

	void EndPlay_Implementation() override;

	void Deinitialize_Implementation() override;
};
```
### 2.2在C++中获取单例实例
#### 2.2.1通过蓝图函数库方法获取单例实例
```C++
	if (USingletonBase* CppSingleton = USingletonBlueprintLibrary::GetSingleton(GetWorld(), UCppSingletonExample::StaticClass()))
	{
		Cast<UCppSingletonExample>(CppSingleton)->GetNowTime();
	}
```
#### 2.2.2通过单例系统获取单例实例
```C++
	if (USingletonSystem* System = GetWorld()->GetGameInstance()->GetSubsystem<USingletonSystem>())
	{
		System->GetSingleton<UCppSingletonExample>()->GetNowTime();
	}
```
### 3.在蓝图中使用
#### 3.1首先确认插件已开启
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210525093832.png)
#### 3.2创建蓝图单例类
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/2021-05-25_093208.png)
#### 3.3创建蓝图节点
#### 3.3.1按住Shif+S，再单击鼠标左键，可快捷创建节点
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/2021-05-25_095824.png)
#### 3.3.2也可以通过普通方式，右键单击输入关键字，Singleton进行搜索
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/2021-05-25_100140.png)
#### 3.4在SingletonClass下来菜单中选择单例类，便能返回该单例实例，无需再次转换
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210525095750.png)
