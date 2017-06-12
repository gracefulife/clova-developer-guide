# Summary

## Clova Developer Guide

* [문서 정보](README.md)
* [저작권](Copyright.md)

## Clova Interface Connect

* [CIC 개요](/CIC/CIC_Overview.md)
  * [CIC란?](/CIC/CIC_Overview.md#WhatisCIC)
  * [CIC 동작 구조](/CIC/CIC_Overview.md#CICInteractionStructure)
* [CIC 연동하기](/CIC/Guides/Interact_with_CIC.md)
  * [사전 준비사항](/CIC/Guides/Interact_with_CIC.md#Preparation)
  * [CIC 연결하기](/CIC/Guides/Interact_with_CIC.md#ConnectToCIC)
    * [Clova access token 생성하기](/CIC/Guides/Interact_with_CIC.md#CreateClovaAccessToken)
    * [연결하기](/CIC/Guides/Interact_with_CIC.md#CreateConnection)
    * [인증하기](/CIC/Guides/Interact_with_CIC.md#Authentication)
    * [연결 관리하기](/CIC/Guides/Interact_with_CIC.md#ManageConnection)
  * [이벤트 메시지 전송하기](/CIC/Guides/Interact_with_CIC.md#SendEvent)
  * [지시 메시지 처리하기](/CIC/Guides/Interact_with_CIC.md#HandleDirective)
  * [메시지 큐 관리하기](/CIC/Guides/Interact_with_CIC.md#ManageMessageQ)
* [HTTP/2 메시지 포맷](/CIC/References/HTTP2_Message_Format.md)
  * [HTTP 요청](/CIC/References/HTTP2_Message_Format.md#Request)
  * [HTTP 응답](/CIC/References/HTTP2_Message_Format.md#Response)
  * [HTTP 메시지 예제](/CIC/References/HTTP2_Message_Format.md#MessageExample)
* [Clova 인증 API](/CIC/References/Clova_Auth_API.md)
  * [/authorize](/CIC/References/Clova_Auth_API.md#authorize)
  * [/token](/CIC/References/Clova_Auth_API.md#token)
* [CIC 메시지 포맷](/CIC/References/CIC_Message_Format.md)
  * [이벤트 메시지 \(Event\)](/CIC/References/CIC_Message_Format.md#Event)
  * [지시 메시지 \(Directive\)](/CIC/References/CIC_Message_Format.md#Directive)
* [CIC API](/CIC/References/CIC_API.md)
  * [Alerts](/CIC/References/APIs/Alerts.md)
  * [AudioPlayer](/CIC/References/APIs/AudioPlayer.md)
  * [Clova](/CIC/References/APIs/Clova.md)
  * [Memo](/CIC/References/APIs/Memo.md)
  * [PlaybackController](/CIC/References/APIs/PlaybackController.md)
  * [Reminder](/CIC/References/APIs/Reminder.md)
  * [SpeechRecognizer](/CIC/References/APIs/SpeechRecognizer.md)
  * [SpeechSynthesizer](/CIC/References/APIs/SpeechSynthesizer.md)
  * [이벤트 메시지 색인](/CIC/References/APIs/Index_for_Events.md)
  * [지시 메시지 색인](/CIC/References/APIs/Index_for_Directives.md)
* [맥락 정보(Context)](/CIC/References/Context_Objects.md)
  * [AudioPlayer.PlaybackState](/CIC/References/Context_Objects.md#PlaybackState)
  * [Device.DeviceState](/CIC/References/Context_Objects.md#DeviceState)
  * [Clova.FreetalkState](/CIC/References/Context_Objects.md#FreetalkState)
  * [Clova.Location](/CIC/References/Context_Objects.md#Location)
  * [Clova.SavedPlace](/CIC/References/Context_Objects.md#SavedPlace)
  * [Speaker.VolumeState](/CIC/References/Context_Objects.md#VolumeState)
* [Content Template](/CIC/References/Content_Templates.md)
  * [CardList](/CIC/References/ContentTemplates/CardList.md)
  * [ImageList](/CIC/References/ContentTemplates/ImageList.md)
  * [ImageText](/CIC/References/ContentTemplates/ImageText.md)
  * [Text](/CIC/References/ContentTemplates/Text.md)
  * [Shared Objects](/CIC/References/ContentTemplates/Shared_Objects.md)

## Clova Extension Kit

* [CEK 개요](/CEK_Overview.md)
  * CEK란?
  * CEK 동작 구조
  * Extension 종류
* [Custom Extension 만들기](/CEK/Guides/Build_Custom_Extension.md)
  * Custom Extension이란?
  * 사전 준비 사항
  * Extension 요청 처리
  * Extension 응답 처리
* [Clova Home Extension 만들기](/CEK/Guides/Build_Clova_Home_Extension.md)
  * Clova Home Extension이란?
  * 사전 준비 사항
  * Discovery 제공하기
  * Extension 요청 처리
  * Extension 응답 처리
* [사용자 계정 연동하기](/CEK/Guides/LinkClovaUserToUserInYourService.md)
* [CEK 메시지 포맷](/CEK/References/CEK_Message_Format.md)
  * [HTTP 메시지](/CEK/References/CEK_Message_Format.md#HTTPMessage)
  * [Custom extension 메시지](/CEK/References/CEK_Message_Format.md#CustomExtenstionMessage)
  * [Clova Home extension 메시지](/CEK/References/CEK_Message_Format.md#ClovaHomeExtensionMessage)
* [Clova Home extension API](/CEK/References/Clova_Home_Extension_API.md)
