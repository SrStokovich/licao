Integração Multi-Cloud Azure e Aws

1- Passo a Passo da Configuração da VPN Site-to-Site 🔷 Etapa 1: Configuração no Azure Criar Resource Group: Nome: rg_azure_aws_project | Região: East-US

Criar Virtual Network (VNet): Nome: vnet-azure | CIDR: 192.168.0.0/16 Sub-rede: subnet-01 | CIDR: 192.168.0.0/24

Criar Gateway Subnet: Nome: GatewaySubnet | CIDR: reservado automaticamente pela Azure.

Criar VPN Gateway (Virtual Network Gateway): Nome: vpn-azure-aws Tipo: VPN | SKU: VpnGw1 | IP Público: pip-vpn-azure-aws

Etapa 2: Configuração na AWS Criar VPC: Nome: my-vpc-01 | CIDR: 172.16.0.0/16

Criar Sub-rede: Nome: my-subnet-01 | CIDR: 172.16.0.0/24

Criar Customer Gateway: IP: (IP público do Azure VPN Gateway)

Criar Virtual Private Gateway (VGW): Nome: vpg-aws-azure | Anexado à VPC

Criar Site-to-Site VPN Connection: Nome: vpn-aws-azure Tipo de Gateway: Virtual Private Gateway Customer Gateway: Existente Roteamento: Estático Prefixo IP estático: 192.168.0.0/24 Baixar o arquivo de configuração da VPN (Vendor: Genérico)

Etapa 3: Conectar o Azure à AWS Criar Local Network Gateway no Azure: Nome: lng-azure-aws IP: IP externo da AWS (conforme arquivo de configuração) Espaço de Endereço: 172.16.0.0/16

Criar a Conexão Site-to-Site no Azure: Nome: connection-azure-aws Tipo: Site-to-Site (IPSec) Local Network Gateway: o criado acima Shared Key: (retirada do arquivo de configuração AWS)

Verificar no portal da AWS: Status do túnel: Ativo

Etapa 4: Configurar Rotas e Internet na AWS Criar Internet Gateway: Nome: my-internet-gateway Anexado à VPC.

Configurar Route Table da VPC:

Destino Target 192.168.0.0/24 Virtual Private Gateway 0.0.0.0/0 Internet Gateway

Etapa 5: Criar Máquinas Virtuais e Testar Conectividade Azure: Criar uma VM (exemplo: Linux ou Windows) na sub-rede privada.

AWS: Criar uma instância EC2 Windows ou Linux na sub-rede privada.

Testes realizados: ✅ Ping da VM Azure → EC2 AWS (usando IP privado) ✅ Ping da EC2 AWS → VM Azure (usando IP privado) ✅ SSH ou RDP entre as VMs (se aplicável)
