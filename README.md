# liraserverweb

Liraservia — Sistema MVC Modular em Python 3.12+ com Motor de IA (DDGS), persistência MySQL (PyMySQL) e auditoria automática via triggers.
# Liraservia — Sistema MVC Modular e Motor de IA

Arquitetura Python MVC modular, escalável e segura para o ecossistema **Liraservia**. O sistema mantém separação total entre os módulos antigos de cadastro (CRUD) e os novos componentes de Inteligência Artificial, com banco de dados MySQL e auditoria automática.

---

## Estrutura de Pastas do Projeto

```text
lirarservia_python/
│
├── core/                               # Núcleo da Aplicação
│   ├── llm/                            # Serviço de Inteligência Artificial
│   │   ├── __init__.py
│   │   └── llm_client.py               # Cliente de busca em tempo real (DDGS)
│   ├── __init__.py
│   ├── base_model.py                   # Operações básicas de banco (CRUD) e auditoria
│   ├── config.py                       # Configurações gerais do sistema
│   ├── database.py                     # Conexão com o banco via PyMySQL
│   ├── exceptions.py                   # Tratamento centralizado de erros
│   └── security.py                     # Criptografia e segurança
│
├── modules/                            # Módulos de Negócio Isolados
│   ├── administrativo/
│   │   └── ai/                         # Estrutura MVC da IA no painel Administrativo
│   │       ├── controllers/
│   │       ├── models/
│   │       └── views/
│   └── app/
│       └── ai/                         # Estrutura MVC da IA no Módulo App
│           ├── controllers/
│           │   └── app_ai_controller.py
│           ├── models/
│           │   ├── agent_model.py
│           │   ├── message_model.py
│           │   └── thread_model.py
│           └── views/
│               └── agent_view.py
│
├── routers/                            # Central de Rotas
│   ├── admin_router.py
│   ├── app_router.py
│   └── site_router.py
│
├── shared/                             # Recursos e Utilitários Compartilhados
│   ├── __init__.py
│   ├── constants/                      # Constantes globais e códigos de status
│   │   ├── __init__.py
│   │   └── status_codes.py
│   ├── utils/                          # Funções auxiliares de formatação e limpeza
│   │   ├── __init__.py
│   │   └── formatters.py
│   └── views/                          # Telas e respostas genéricas reutilizáveis
│       └── __init__.py
│
├── .env
├── main.py                             # Arquivo principal que inicia o sistema
├── README.md
└── requirements.txt
Copyright (c) 2026 Robson Santana - SANTANAKOJAK / sr07webdba.santana.
					Todos os direitos reservados.

					AVISO DE PROPRIEDADE E TERMOS DE USO RESTRITIVO  
					(Protegido pela Lei nº 9.609/1998 – Software, Lei nº 9.279/1996 – 
					Propriedade Industrial, Lei nº 12.965/2014 – Marco Civil da Internet, 
					Lei nº 10.603/2002 – Segredo Industrial, Tratados Internacionais de 
					Propriedade Intelectual incluindo a Convenção de Berna e o Acordo 
					TRIPS da OMC, além da Legislação Civil e Penal Brasileira)

					Este software, incluindo seu código-fonte, banco de dados, lógica de 
					negócio, documentação e elementos visuais associados (o "Software"), 
					é de propriedade exclusiva e intelectual do autor Robson Santana.

					A obtenção de uma cópia deste Software confere apenas o direito de 
					visualização e avaliação técnica estritamente pessoal, sob as 
					seguintes condições restritivas:

					PROIBIÇÃO DE CÓPIA E DISTRIBUIÇÃO  
					É terminantemente proibida a cópia, reprodução, modificação, distribuição, 
					publicação, sublicenciamento, aluguel ou transferência do Software, no 
					todo ou em parte, para terceiros, por qualquer meio físico ou digital, 
					nos termos da Lei nº 9.609/98 e dos tratados internacionais aplicáveis
					(Convenção de Berna e TRIPS/OMC).

					PROIBIÇÃO DE USO COMERCIAL E FINANCEIRO  
					É expressamente proibida a utilização deste Software, de sua lógica 
					estrutural ou de suas derivações para quaisquer fins comerciais, 
					industriais, de prestação de serviços a terceiros, ou para a obtenção 
					de qualquer forma de lucro financeiro, direto ou indireto, sem a 
					autorização prévia e expressa por escrito do detentor dos direitos autorais.

					ENGENHARIA REVERSA  
					É vedada a realização de engenharia reversa, descompilação, desmontagem ou
					tentativa de extração do código-fonte ou do modelo lógico do Software, 
					aracterizando violação de segredo industrial (Lei nº 10.603/02 e Código Penal).

					CLÁUSULA DE PENALIDADE E INDENIZAÇÃO  
					O uso indevido, a cópia não autorizada ou a exploração comercial e financeira 
					em desacordo com estes termos sujeitará o infrator ao pagamento de indenização 
					por perdas e danos materiais e morais, além de multa compensatória equivalente 
					a 10 (dez) vezes o valor de mercado do sistema, definido por preço de tabela 
					vigente, contrato firmado ou avaliação pericial, prevalecendo o maior valor. 
					Esta cláusula aplica-se também em jurisdições internacionais que reconheçam 
					tratados de propriedade intelectual, sem prejuízo das sanções penais cabíveis.

					FORO E LEGISLAÇÃO APLICÁVEL  
					Este termo é regido pelas leis da República Federativa do Brasil, pelo Marco 
					Civil da Internet e pelos tratados internacionais de proteção à propriedade 
					intelectual (Convenção de Berna e TRIPS/OMC). Fica eleito o foro da Comarca 
					do Rio de Janeiro, Estado do Rio de Janeiro, com renúncia expressa a qualquer 
					outro, por mais privilegiado que seja, para dirimir qualquer litígio decorrente
					deste instrumento.

					O SOFTWARE É FORNECIDO “NO ESTADO EM QUE SE ENCONTRA”, SEM QUALQUER TIPO DE 
					GARANTIA, EXPRESSA OU IMPLÍCITA, INCLUINDO, MAS NÃO SE LIMITANDO ÀS GARANTIAS 
					DE COMERCIALIZAÇÃO, ADEQUAÇÃO A UM PROPÓSITO ESPECÍFICO E NÃO VIOLAÇÃO. EM 
					NENHUMA HIPÓTESE O AUTOR OU DETENTORES DOS DIREITOS AUTORAIS SERÃO RESPONSÁVEIS 
					POR QUALQUER REIVINDICAÇÃO, DANO OU OUTRA RESPONSABILIDADE, SEJA EM AÇÃO DE 
					CONTRATO, ATO ILÍCITO OU OUTRA FORMA, DECORRENTE DE, OU RELACIONADA AO SOFTWARE 
					OU AO USO OU OUTRAS NEGOCIAÇÕES NO SOFTWARE.
