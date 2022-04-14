# Pranks

## Prank 1

```Powershell
#Run this every 1/2 hour and in an 8 hour work day there will be approximately 3 times per day that your victim hears a cat fact
if ((Get-Random -Maximum 10000) -lt 1875) {
    Add-Type -AssemblyName System.Speech
    $SpeechSynth = New-Object System.Speech.Synthesis.SpeechSynthesizer
    $CatFact = (ConvertFrom-Json (Invoke-WebRequest -Uri 'http://catfacts-api.appspot.com/api/facts')).facts
    $SpeechSynth.Speak("did you know?")
    $SpeechSynth.Speak($CatFact)
}    
```

## Prank 2

```Powershell
Add-Type -AssemblyName System.Speech
$SpeechSynth = New-Object System.Speech.Synthesis.SpeechSynthesizer
$SpeechSynth.Speak("Just what do you think you're doing, Dave?")
```

## Prank 3

```Powershell
$j1 = Start-Job {
    Add-Type -AssemblyName System.Speech
    $SpeechSynth = New-Object System.Speech.Synthesis.SpeechSynthesizer
    $SpeechSynth.SelectVoiceByHints('Male')
    $SpeechSynth.Speak("Row, Row, Row your boat gently down the stream.  Merrily! Merrily! Merrily! Life is but a dream.")
}
Start-Sleep -Seconds 1
$j2 = Start-Job {
    Add-Type -AssemblyName System.Speech
    $SpeechSynth = New-Object System.Speech.Synthesis.SpeechSynthesizer
    $SpeechSynth.SelectVoiceByHints('Female')
    $SpeechSynth.Speak("Row, Row, Row your boat gently down the stream.  Merrily! Merrily! Merrily! Life is but a dream.")
}
$j1,$j2 | Wait-Job | Receive-Job
$j1,$j2 | Remove-Job
```

## Prank 4

```Powershell
$Scriptblock = {
    Add-Type -AssemblyName System.Speech
    $SpeechSynth = New-Object System.Speech.Synthesis.SpeechSynthesizer
    $CatFact = (ConvertFrom-Json (Invoke-WebRequest -Uri 'http://catfacts-api.appspot.com/api/facts' -UseBasicParsing)).facts
    $SpeechSynth.Speak("did you know?")
    $SpeechSynth.Speak($CatFact)
}

Invoke-Command -ComputerName VictimPC -ScriptBlock $Scriptblock
```

## Prank 5

darthvader

```Powershell
start-job {
[console]::beep(440,500)
[console]::beep(440,500)
[console]::beep(440,500)
[console]::beep(349,350)
[console]::beep(523,150)
[console]::beep(440,500)
[console]::beep(349,350)
[console]::beep(523,150)
[console]::beep(440,1000)
[console]::beep(659,500)
[console]::beep(659,500)
[console]::beep(659,500)
[console]::beep(698,350)
[console]::beep(523,150)
[console]::beep(415,500)
[console]::beep(349,350)
[console]::beep(523,150)
[console]::beep(440,1000)
}
```

## Prank 3

Super Mario!

```Powershell
function b($a,$b){
    [console]::beep($a,$b)
}
function s($a){
    sleep -m $a
}
write-host "Super Mario!"
b 660 100;
s 150;
b 660 100;
s 300;
b 660 100;
s 300;
b 510 100;
s 100;
b 660 100;
s 300;
b 770 100;
s 550;
b 380 100;
s 575;

b 510 100;
s 450;
b 380 100;
s 400;
b 320 100;
s 500;
b 440 100;
s 300;
b 480 80;
s 330;
b 450 100;
s 150;
b 430 100;
s 300;
b 380 100;
s 200;
b 660 80;
s 200;
b 760 50;
s 150;
b 860 100;
s 300;
b 700 80;
s 150;
b 760 50;
s 350;
b 660 80;
s 300;
b 520 80;
s 150;
b 580 80;
s 150;
b 480 80;
s 500;

b 510 100;
s 450;
b 380 100;
s 400;
b 320 100;
s 500;
b 440 100;
s 300;
b 480 80;
s 330;
b 450 100;
s 150;
b 430 100;
s 300;
b 380 100;
s 200;
b 660 80;
s 200;
b 760 50;
s 150;
b 860 100;
s 300;
b 700 80;
s 150;
b 760 50;
s 350;
b 660 80;
s 300;
b 520 80;
s 150;
b 580 80;
s 150;
b 480 80;
s 500;

b 500 100;
s 300;

b 760 100;
s 100;
b 720 100;
s 150;
b 680 100;
s 150;
b 620 150;
s 300;

b 650 150;
s 300;
b 380 100;
s 150;
b 430 100;
s 150;

b 500 100;
s 300;
b 430 100;
s 150;
b 500 100;
s 100;
b 570 100;
s 220;

b 500 100;
s 300;

b 760 100;
s 100;
b 720 100;
s 150;
b 680 100;
s 150;
b 620 150;
s 300;

b 650 200;
s 300;

b 1020 80;
s 300;
b 1020 80;
s 150;
b 1020 80;
s 300;

b 380 100;
s 300;
b 500 100;
s 300;

b 760 100;
s 100;
b 720 100;
s 150;
b 680 100;
s 150;
b 620 150;
s 300;

b 650 150;
s 300;
b 380 100;
s 150;
b 430 100;
s 150;

b 500 100;
s 300;
b 430 100;
s 150;
b 500 100;
s 100;
b 570 100;
s 420;

b 585 100;
s 450;

b 550 100;
s 420;

b 500 100;
s 360;

b 380 100;
s 300;
b 500 100;
s 300;
b 500 100;
s 150;
b 500 100;
s 300;

b 500 100;
s 300;

b 760 100;
s 100;
b 720 100;
s 150;
b 680 100;
s 150;
b 620 150;
s 300;

b 650 150;
s 300;
b 380 100;
s 150;
b 430 100;
s 150;

b 500 100;
s 300;
b 430 100;
s 150;
b 500 100;
s 100;
b 570 100;
s 220;

b 500 100;
s 300;

b 760 100;
s 100;
b 720 100;
s 150;
b 680 100;
s 150;
b 620 150;
s 300;

b 650 200;
s 300;

b 1020 80;
s 300;
b 1020 80;
s 150;
b 1020 80;
s 300;

b 380 100;
s 300;
b 500 100;
s 300;

b 760 100;
s 100;
b 720 100;
s 150;
b 680 100;
s 150;
b 620 150;
s 300;

b 650 150;
s 300;
b 380 100;
s 150;
b 430 100;
s 150;

b 500 100;
s 300;
b 430 100;
s 150;
b 500 100;
s 100;
b 570 100;
s 420;

b 585 100;
s 450;

b 550 100;
s 420;

b 500 100;
s 360;

b 380 100;
s 300;
b 500 100;
s 300;
b 500 100;
s 150;
b 500 100;
s 300;

b 500 60;
s 150;
b 500 80;
s 300;
b 500 60;
s 350;
b 500 80;
s 150;
b 580 80;
s 350;
b 660 80;
s 150;
b 500 80;
s 300;
b 430 80;
s 150;
b 380 80;
s 600;

b 500 60;
s 150;
b 500 80;
s 300;
b 500 60;
s 350;
b 500 80;
s 150;
b 580 80;
s 150;
b 660 80;
s 550;

b 870 80;
s 325;
b 760 80;
s 600;

b 500 60;
s 150;
b 500 80;
s 300;
b 500 60;
s 350;
b 500 80;
s 150;
b 580 80;
s 350;
b 660 80;
s 150;
b 500 80;
s 300;
b 430 80;
s 150;
b 380 80;
s 600;

b 660 100;
s 150;
b 660 100;
s 300;
b 660 100;
s 300;
b 510 100;
s 100;
b 660 100;
s 300;
b 770 100;
s 550;
b 380 100;
s 575;
```	

## Prank 7  

```Powershell
while(1) 
{
    Start-Process 'http://www.google.com/'
}
```