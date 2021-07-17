{{$name := .Get 0}}
{{$verPat := "\\d+(\\.\\d+)+"}}
{{$rawNvdaUrl := index $.Page.Site.Data.urls.voices.nvda $name}}
{{$nvdaUrl := urls.Parse $rawNvdaUrl}}
{{$nvdaVer := index (findRE $verPat $nvdaUrl.Path) 0}}
[{{i18n "nvdaVoiceLink"}}]({{$rawNvdaUrl}}), {{i18n "versionX" (dict "version" $nvdaVer)}}
{{$rawSapiUrl := index $.Page.Site.Data.urls.voices.sapi $name}}
{{$sapiUrl := urls.Parse $rawSapiUrl}}
{{$sapiVer := index (findRE $verPat $sapiUrl.Path) 0}}
[{{i18n "sapiVoiceLink"}}]({{$rawSapiUrl}}), {{i18n "versionX" (dict "version" $sapiVer)}}
