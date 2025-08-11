# Gerenciamento de Máquinas Virtuais no Azure
Anotações de estudo sobre o gerenciamento de máquinas virtuais no Azure, com foco na certificação AZ-104, e definições de disponibilidade das VMs.

O ideal é que já exita um ```Resource Group``` com as  ```Virtual Networks``` necessárias já configuradas antes de adicionar as ```Virtual Machines```. Porém, como a finalidade é documentar as configurações de ```Availability optins``` e gerencimanto de ```Familias(SKU)``` das VMs, vou deixar deixar a configuração da rede ser configurada na criação das VMs.

## Availability Options (Opções de Disponibilidade)

|Opção|Descrição|Quando Usar|
|-|-|-|
|No infrastructure redundancy required|A VM não criada não terá alta disponibilidade em casos de falhas|Em ambientes de testes|
|Availability Zone|A VM é distribuída entre zonas físicas(Data Centers) separadas dentro da mesma região Azure, garantindo alta disponibilidade contra falhas de datacenter|Para aplicações críticas que exigem alta resiliência e disponibilidade|
|Availability Set|Separa as VMs em diferentes racks físicos dentro do mesmo datacenter, protegendo contra falhas de hardware e sistema|Ideal para aplicações que precisam de SLA elevado, sem separação geográfica|
|Virtual Machine Scale Set (VMSS)|Conjunto de VMs idênticas que podem escalar automaticamente com base na demanda. Pode ser integrado com Availability Zones.|Aplicações distribuídas e cargas que variam com o tempo. Ideal para alta escalabilidade e automação|

> 💡 Usar Availability Zones pode garantir até 99.99% de SLA, enquanto Availability Sets oferecem até 99.95%.

## Familias(SKUs) de Máquinas Virtuais no Azure

| Categoria | Descrição | Exemplos de SKU | Casos de Uso |
|-|-|-|-|
| **General Purpose** | Balanceamento entre CPU e memória. | B, Dsv3, Dv4, Dasv5 | Web servers, ambientes de desenvolvimento/teste, aplicações empresariais. |
| **Compute Optimized** | Alta performance de CPU. | Fsv2 | Processamento intensivo, servidores de aplicação, cargas de trabalho computacionais. |
| **Memory Optimized** | Alta capacidade de memória por vCPU. | Esv3, Ev4, M series | Bancos de dados, caches em memória, análise de grandes volumes de dados. |
| **Storage Optimized** | Alta taxa de IOPS e throughput de disco. | Lsv2 | Bancos de dados NoSQL, armazenamento de dados em larga escala, aplicações que exigem acesso rápido ao disco. |
| **GPU** | Equipadas com GPUs para cargas gráficas ou paralelas. | NC, ND, NV series | Machine learning, renderização gráfica, simulações científicas, jogos. |
| **High Performance Compute (HPC)** | Baixa latência e alta performance para computação científica. | H series, HB, HC | Modelagem molecular, simulações físicas, engenharia computacional. |

> ℹ️ Os SKUs variam em número de vCPUs, memória, tipo de disco, suporte a rede acelerada, entre outros. Sempre verifique a compatibilidade com sua carga de trabalho.

## Configuração da VM no portal Azure

Conhecendo as opções disponibilidade e familias(SKUs) de máquinas disponíveis, optei por seguir com uma opção de baixo custo e optei pela opção ```availability set``` com 3 ```Fault domain```(Dominios de Falhas, ou racks) e 5 ```Update domains```(hosts). 
<img width="1803" height="849" alt="image" src="https://github.com/user-attachments/assets/7bc39971-125c-46bc-acd8-e01af420b7cc" />

A imagem abaixo ilustra a disposição de racks e maquinas para a configuração apresentada no print acima:

![Diagrama de Fault Domains e Update Domains](https://i.sstatic.net/fqdkn.png)

> 📌 Este diagrama mostra a distribuição de *Update Domains* e *Fault Domains* em um ambiente de alta disponibilidade no Azure.  
> Fonte: [Documentação oficial da Microsoft Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/availability-set-overview)


### 📚 Links da documentação oficial da Microsoft para estudo:

- [Availability Set](https://learn.microsoft.com/en-us/azure/virtual-machines/availability-set-overview)
- [Familias SKUs](https://learn.microsoft.com/en-us/azure/virtual-machines/dedicated-hosts-how-to?tabs=portal)

## Tecnologias utilizadas:

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=azure&logoColor=white) ![Azure VM](https://img.shields.io/badge/Azure%20VMs-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white) ![Availability Set](https://img.shields.io/badge/Availability%20Set-99.95%25%20SLA-blue?style=for-the-badge) ![Availability Zones](https://img.shields.io/badge/Availability%20Zones-99.99%25%20SLA-green?style=for-the-badge) ![AZ-104](https://img.shields.io/badge/AZ--104-Study%20Guide-purple?style=for-the-badge)
