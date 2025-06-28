# Guia de estudos para o exame de certificação da Microsoft Azure Administrator (AZ-104)

## Máquinas Virtuais
### 🧱 1. Planejamento e Pré-requisitos
- Escolha da imagem da VM: Windows, Linux ou customizada, disponível no Azure Marketplace ou como VHD.
- Tamanho da VM: Baseado em CPU, RAM, IOPS e throughput (séries D, E, M, etc.).
- Localização: Selecionar Região/Availability Zone (AZ) apropriadas.
- Serviços de suporte: Rede Virtual (VNet) e subnets designados; Grupo de Segurança de Rede (NSG) ou Application Security Groups (ASG) ; Regras de roteamento e NSG aplicados.
- Storage: Discos gerenciados (Premium SSD, Standard SSD/HDD) anexados como dados ou SO; Considerar Ultra Disk ou discos replicados para cenários críticos.

### ⚙️ 2. Criação de VM
#### 2.1 Via Portal Azure
- Escolher Resource Group, Região e imagem.
- Selecionar tamanho e configurar admin user (senha ou SSH).
- Configurar discos e network (VNet, subnet, IP público/privado, NSG, ASG).
- Revisar e criar vm.

#### 2.2 Via CLI/Powershell/ARM Template/Bicep/Terraform
Uso de az vm create, scripts ARM ou Bicep, ou definição de Terraform.

#### 2.3 Extensões e scripts de inicialização
Extensões: Custom Script, Azure VM Agent, Azure Policy, para pós-criação (ex.: instalar software, configurações de segurança, definição de backup).

### 🧩 3. Configuração Pós-Criação
Atualização do OS e aplicação de patches.

Configurar backup via Azure Backup.

Monitoramento: ativar Guest diagnostic, métricas no Azure Monitor e logs no Log Analytics.

Instalar agentes como:

Azure Monitor Agent (AMA)

Microsoft Defender for Cloud

Antivírus/EDR

Customização de segurança: firewall, usuários, SELinux/AppArmor, roles.

### 🔒 4. Requisitos de Rede
IPs: público (opcional) e privado.

NSG/ASG configurado de acordo com funções da VM.

USar DNS interno e Azure DNS (opcional).

Conexão com redes on-premises via VPN ou ExpressRoute (opcional).

### 🔄 5. Backup e Recuperação de Desastres
Azure Backup para proteção de dados via snapshots e recovery points.

Azure Site Recovery (ASR) para replicação entre regiões e failover de VM como parte da estratégia de DR.

### 📈 6. Alta Disponibilidade (HA)
6.1 Deploy em Availability Sets
Configurar Fault Domains (FD) e Update Domains (UD) para evitar falhas de rack, rede e manutenção simultânea.

6.2 Deploy em Availability Zones (AZs)
Implantar VMs em subnets diversas ligadas a zonas diferentes dentro da mesma região para resiliência geográfica local.

6.3 Load Balancers / Application Gateway
Azure Load Balancer: balanceamento de TCP/UDP entre VMs.

Azure Application Gateway: balanceamento com inspeção L7, WAF etc.

6.4 Scale Sets (VMSS)
Criação de grupos de VMs idênticas com auto-scaling, configuradas para HA com zonas ou availability sets.

6.5 Virtual Machine Availability Zones + Scale Set
Criação conjunta para redundância e escalabilidade.

### 🧾 7. Manuseio e Operações de Rotina
Escalonamento (vertical/horizontal): aumentar tamanho ou número de VMs.

Redimensionamento com detachment e reattachment de discos.

Snapshots e Managed Images para cenários de PaaS personalizados.

Patching com Azure Update Manager.

### 📊 8. Monitoramento e Logs
Métricas: CPU, disco, rede, IOPS no Azure Monitor.

Logs: boot diagnostics, activity log, guest diagnostic.

Aplicações: logs no Log Analytics; dashboards personalizados.

Criação de alertas com Action Groups por e-mail/SMS/webhook/etc.

### 🔌 9. Automação e DevOps
Uso de ARM/Bicep/Terraform, Azure Policy para governança e compliance.

Pipelines (Azure DevOps/GitHub Actions) para deployment repetível.

Uso de Tags para organização e custo.

Lifecycle na CI/CD para implantação e desativação.

### 🧰 10. Segurança e Conformidade
Defender for Cloud: hardening e recomendações.

Azure Policy evaluando tipo de VM, storage criptografado, extensão de agentes etc.

Identity control: acesso via RBAC, Azure Bastion, MFA e managed identities.

NSG/ASG possibilitando controle mínimo de privilégios.

Encryption: Data-at-rest (Encryption at host, Azure Disk Encryption) e Data-in-transit.

### ✅ Resumo – Cenários de Alta Disponibilidade
| Estratégia HA                    | Componente                                         |
| -------------------------------- | -------------------------------------------------- |
| **Availability Set**             | Proteção contra falhas locais                      |
| **Availability Zone**            | Isolamento geográfico dentro da região             |
| **Load Balancer / App Gateway**  | Disponibilidade e balanceamento de carga           |
| **Scale Sets + Zones**           | Escalabilidade + alta disponibilidade automatizada |
| **VMSS + DevOps**                | Automação de criação e gestão                      |
| **Backup + Site Recovery**       | Continuidade de negócio na falha                   |
| **Azure Policy + Monitoramento** | Detecção e conformidade contínua                   |
