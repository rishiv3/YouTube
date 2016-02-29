# YouTube

````
$Playlisturl = &quot;http://www.youtube.com/playlist?list=PL1058E06599CCF54D&quot; //any
$VideoUrls= (invoke-WebRequest -uri $Playlisturl).Links | ? {$_.HREF -like &quot;/watch*&quot;} | ` 
? innerText -notmatch &quot;.[0-9]:[0-9].&quot; | ? {$_.innerText.Length -gt 3} | Select innerText, ` 
@{Name=&quot;URL&quot;;Expression={'http://www.youtube.com' + $_.href}} | ? innerText -notlike &quot;*Play all*&quot;
 
$VideoUrls
 
ForEach ($video in $VideoUrls){
Write-Host (&quot;Downloading &quot; + $video.innerText)
.\youtube-dl.exe $video.URL
}
````
