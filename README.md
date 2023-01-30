# htmlgui.ahk
Very simple autohotkey GUI with HTML &amp; CSS
```
#NoEnv
#SingleInstance Force
Title := "Create GUI with HTML & CSS"
Gui Add, ActiveX, x0 y0 w400 h200 vWB, Shell.Explorer
wb.navigate("about:<!DOCTYPE html><meta http-equiv='X-UA-Compatible' content='IE=edge'><body></body>")
while wb.busy || wb.readystate<4
Sleep, 20

HTML =
( LTrim
	<style>
		body,h3,table{margin:0 auto; text-align:center}
		button{position: relative}
	</style>
	<br/><h3>Set Initial Inputs</h3><br/>
	<table id="table" align="center"></table>
)
doc := wb.document
doc.body.innerhtml := HTML

email := {CallingCode:880, FirstNumber:01711456131, LastNumber:01711556131}
for key, val in email
{
	tr := doc.createElement("tr")
	td := doc.createElement("td")
	in := doc.createElement("input")
	in.id := key
	in.value := val
	in.placeholder := key
	td.appendChild(in)
	tr.appendChild(td)
	doc.getElementById("table").appendChild(tr)
}

div := doc.createElement("div")
div.innerHTML := "<br /><button id='update'>Update Settings</button>"
doc.body.appendChild(div)

update := doc.getElementById("update")
ComObjConnect(update, "Update_")

Gui, 1:+LastFoundExist
WinExist()
WinSetTitle % Title
Gui Show, w400 h200
Return
GuiClose:
ExitApp

Update_OnClick(){
	Global doc
	cccode := doc.getElementById("CallingCode").value
	fphone := doc.getElementById("FirstNumber").value
	lphone := doc.getElementById("LastNumber").value
	MsgBox %cccode% %fphone% %lphone%
}
```
