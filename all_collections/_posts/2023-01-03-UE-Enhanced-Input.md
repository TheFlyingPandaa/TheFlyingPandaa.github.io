---
layout: post
title: UE5 C++ Enhanced Input quick start 
date: 2023-01-03
categories: ["Unreal", "Enhanced input", "C++", "first post"]
---

# Steps 

1.  Adding dependency
2.  Setting up the player
3.  Setting up the assets

## 1 Adding dependency

You need to add `EnhancedInput` into your Dependency module

> *ProjectName*.build.cs

```cs
PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "EnhancedInput" });
```

## 2 Setting up the player

You need a `UInputMappingContext` and a `UInputAction`

> *YourPlayer*.h

```c++
#include "EnhancedInputComponent.h"
#include "EnhancedInputSubsystems.h"

UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Input, meta=(AllowPrivateAccess = "true"))
class UInputMappingContext* DefaultMappingContext;

UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Input, meta=(AllowPrivateAccess = "true"))
class UInputAction* YourAction;
```

> *YourPlayer*.cpp

```c++
void AYourPlayer::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    UEnhancedInputComponent* Input = Cast<UEnhancedInputComponent>(PlayerInputComponent);
    Input->BindAction(YourAction, ETriggerEvent::Triggered, this, &AYourPlayer::Action);
}

void AFooBar::Action(const FInputActionInstance& Instance)
{
    //Types available
    FVector
    FVector2D
    float 
    bool
    //You get it by doing Instance.GetValue()
    //And then insert the Type
    Instance.GetValue().Get<bool>();
} 
```

## 3 Setting up the assets

Create one **Input Mapping Context** and one **Input Action**.
![Blog page]({{site.baseurl}}/assets/pics/InputCreate.png)

Setup your input action to reflect your purpose
![Blog page]({{site.baseurl}}/assets/pics/InputActionPick.png)

Now add the the InputAction and pick a Key to map it to.
![Blog page]({{site.baseurl}}/assets/pics/MappingContextCreate.png)

Now bind the assets to your player
![Blog page]({{site.baseurl}}/assets/pics/PlayerInputBinding.png)









