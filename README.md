# Gerenciamento de Máquinas Virtuais no Azure
Anotações de estudo sobre o gerenciamento de máquinas virtuais no Azure, com foco na certificação AZ-104, e definições de disponibilidade das VMs.

O ideal é que já exita um ```Resource Group``` com as  ```Virtual Networks``` necessárias já configuradas antes de adicionar as ```Virtual Machines```. Porém, como a finalidade é documentar as configurações de ```Availability optins``` e gerencimanto de ```SKU``` das ```Virtual Machines```, vou deixar deixar a configuração da rede ser configurada na criação das VMs.

## Criação das Virtual Machines

### Availability Options (Opções de Disponibilidade)

|Opção|Descrição|Quando Usar|
|-|-|-|
|No infrastructure redundancy required|A VM não criada não terá alta disponibilidade em casos de falhas|Em ambientes de testes|
|Availability Zone|A VM é distribuída entre zonas físicas(Data Centers) separadas dentro da mesma região Azure, garantindo alta disponibilidade contra falhas de datacenter|Para aplicações críticas que exigem alta resiliência e disponibilidade|
|Availability Set|Separa as VMs em diferentes racks físicos dentro do mesmo datacenter, protegendo contra falhas de hardware e sistema|Ideal para aplicações que precisam de SLA elevado, sem separação geográfica|
|Virtual Machine Scale Set (VMSS)|Conjunto de VMs idênticas que podem escalar automaticamente com base na demanda. Pode ser integrado com Availability Zones.|Aplicações distribuídas e cargas que variam com o tempo. Ideal para alta escalabilidade e automação|

> 💡 Usar Availability Zones pode garantir até 99.99% de SLA, enquanto Availability Sets oferecem até 99.95%.

### Categorias de SKUs de Máquinas Virtuais no Azure

| Categoria | Descrição | Exemplos de SKU | Casos de Uso |
|----------|-----------|------------------|--------------|
| **General Purpose** | Balanceamento entre CPU e memória. | B, Dsv3, Dv4, Dasv5 | Web servers, ambientes de desenvolvimento/teste, aplicações empresariais. |
| **Compute Optimized** | Alta performance de CPU. | Fsv2 | Processamento intensivo, servidores de aplicação, cargas de trabalho computacionais. |
| **Memory Optimized** | Alta capacidade de memória por vCPU. | Esv3, Ev4, M series | Bancos de dados, caches em memória, análise de grandes volumes de dados. |
| **Storage Optimized** | Alta taxa de IOPS e throughput de disco. | Lsv2 | Bancos de dados NoSQL, armazenamento de dados em larga escala, aplicações que exigem acesso rápido ao disco. |
| **GPU** | Equipadas com GPUs para cargas gráficas ou paralelas. | NC, ND, NV series | Machine learning, renderização gráfica, simulações científicas, jogos. |
| **High Performance Compute (HPC)** | Baixa latência e alta performance para computação científica. | H series, HB, HC | Modelagem molecular, simulações físicas, engenharia computacional. |

> ℹ️ Os SKUs variam em número de vCPUs, memória, tipo de disco, suporte a rede acelerada, entre outros. Sempre verifique a compatibilidade com sua carga de trabalho.

<img width="1072" height="703" alt="image" src="https://github.com/user-attachments/assets/426b33fa-a3e4-4627-8550-42eca73ca95b" />
