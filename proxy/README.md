# CONFIGURE VPN ON WINDOWS

The following instructions will help you to configure the VPN for the Windows Power Shell bash.


To configure the VPN on Windows you need to create a bash profile

## 1. Creating the bash profile

In a terminal run the following

```bash
code $profile 
```
This will open VisualStudioCode in the Profile file. Inside it you must copy the following code:

It is important that you change the $telusProxy variable to the VPN address provided by your technical leader.

*you have to change*

- *WRITE_THE_PROXY*
- *,SITES_IGNORED_BY_PROXY*

*In the following code*

```bash
function SetProxy() {
  $telusProxy = "WRITE_THE_PROXY"
  $env:http_proxy = $telusProxy
  $env:https_proxy = $telusProxy
  $env:no_proxy = "localhost, .docker.io,.gcr.io   ,SITES_IGNORED_BY_PROXY"
  Write-Output("Proxy set to: " + $telusProxy);
}

function UnSetProxy() {
  Remove-Item Env:\http_proxy
  Remove-Item Env:\https_proxy
  Remove-Item Env:\no_proxy
  refreshenv
}

Set-Alias -Name proxy -Value SetProxy -Description 'Set TELUS Proxy'
Set-Alias -Name removeproxy -Value UnSetProxy -Description 'Remove TELUS Proxy'
```

You can open a new console and it will already load these functions we have just added. 

If you want to use the same console to test the following steps, you must force the console you are in to reload the profile file, to do this run: 

```bash
. $profile
```

## 2. Set the proxy (on each terminal)

Run 

```bash
proxy
```

## 3. Unset the proxy (on each terminal)

Run 

```bash
removeproxy
```

