
# Print Helper
---
### 1. Introduction

Simple and convenient log output statements
### 2. Used in c + +
### 2. 1In c + + to create a Singleton class, see UCpp Singleton Example Example
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
### 2.2 In c + + for singleton instance
#### 2.2.1 Obtained by USingletonBlueprintLibrary get singleton instance
```C++
	if (USingletonBase* CppSingleton = USingletonBlueprintLibrary::GetSingleton(GetWorld(), UCppSingletonExample::StaticClass()))
	{
		Cast<UCppSingletonExample>(CppSingleton)->GetNowTime();
	}
```
#### 2.2.2 Through the USingletonSystem get singleton instance
```C++
	if (USingletonSystem* System = GetWorld()->GetGameInstance()->GetSubsystem<USingletonSystem>())
	{
		System->GetSingleton<UCppSingletonExample>()->GetNowTime();
	}
```
### 3. Used in the blueprint
#### 3.1 First of all confirm the plug-in has been open
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210525093832.png)
#### 3.2 Create a blueprint for singleton class
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/2021-05-25_093208.png)
#### 3.3 Create a blueprint for the node
#### 3.3.1 Hold down shift + S while, and then click the left mouse button, can quickly create nodes. Once the plug-in is enabled, you need to restart the engine again to create the node using the shortcut keys properly, because the plug-in is loaded into a configuration file, which is not loaded until the engine is started
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/2021-05-25_095824.png)
#### 3.3.2 Can also through common mode, right-click on the input keywords, a search for a Singleton
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/2021-05-25_100140.png)
#### 3.4 The Singleton Class down menu Singleton Class, can return to the Singleton instance, need not again
![tool-manager](https://ys-ue4-pluginmall.oss-cn-chengdu.aliyuncs.com/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210525095750.png)

## Support: 1655753014@qq.com

