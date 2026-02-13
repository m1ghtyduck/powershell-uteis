# 🛡️ PowerShell for SOC Analysts & Security Research

Este repositório contém uma coleção de comandos e scripts de PowerShell voltados para a triagem rápida de incidentes, análise de artefatos e monitoramento de ativos em ambientes Windows.

---

## 1. File System & Alternate Data Streams (ADS)
Investigação de técnicas de ocultação de arquivos e persistência.

| Objetivo | Comando | Uso no SOC |
| :--- | :--- | :--- |
| **Listar Streams Ocultos** | `Get-Item -Path "arquivo.exe" -Stream *` | Identifica se há executáveis ou scripts escondidos num arquivo legítimo. |
| **Verificar Origem Web** | `Get-Content -Path "arquivo.zip" -Stream Zone.Identifier` | Confirma se o arquivo veio da internet (ZoneId=3 indica download externo). |
| **Remover Stream Suspeito** | `Remove-Item -Path "doc.pdf" -Stream "MaliciousStream"` | Limpa fluxos de dados sem apagar o arquivo principal. |
| **Integridade (Hash)** | `Get-FileHash -Algorithm SHA256 .\suspicious.ps1` | Gera o hash para verificação em bases de Threat Intelligence. |

---

## 2. Processos, Serviços e Persistência
Identificação de processos anômalos ou validação de agentes de segurança.

### Validar Agentes de Segurança (CrowdStrike / Forti)
```powershell
Get-Service | Where-Object { $_.DisplayName -like "*Forti*" -or $_.DisplayName -like "*Crowd*" }


