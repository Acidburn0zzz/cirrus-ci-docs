# Windows Containers

It is possible to run Windows Containers the same way one can run [Linux containers](/guide/linux.md) on Windows Community Cluster. 
Simply use `windows_container` instead of `container` in `.cirrus.yml` files:

```yaml
windows_container:
  image: cirrusci/windowsservercore:2016
  
task:
  script: ...
```

Cirrus CI will execute [scripts instructions](/guide/writing-tasks.md#script-instruction) like **Batch scripts**.
    
!!! warning "Limitations"
    At the moment only Docker images based of `microsoft/windowsservercore:ltsc2016` are supported since Windows Containers
    are executed via [Azure Container Instances](/guide/supported-computing-services.md#azure-container-instances) computing
    service.
    
# Powershell support

By default Cirrus CI agent executed scripts using `cmd.exe`. It is possible to override default shell executor by providing
`CIRRUS_SHELL` [environment variable](/guide/writing-tasks.md#environment-variables):

```yaml
env:
  CIRRUS_SHELL: powershell
``` 

It is also possible to use *powershell* scripts inline inside of a script instruction by prefixing it with `ps`:

```yaml
windows_container:
  script:
    - ps: Get-Location
```

`ps: COMMAND` is a simple syntactic sugar which transforms it to 

```bash
powershell.exe -EncodedCommand base64(COMMAND)
```
