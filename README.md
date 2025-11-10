# Mottu Challenge - Testes Sprint 4

Larissa de Freitas Moura - 555136
Guilherme Francisco - 557648

## Links Importantes

**Azure DevOps Test Plan:**
https://dev.azure.com/Mottu-MS/Mottu-Challenge/_testPlans/execute?planId=163&suiteId=165

**Azure DevOps Boards:**
https://dev.azure.com/Mottu-MS/Mottu-Challenge/_backlogs/backlog/Mottu-Challenge%20Team/Epics?showParents=true

---

## 🎯 VISÃO GERAL

Baseado no seu backlog no Azure DevOps, vamos criar testes manuais e automatizados para as principais funcionalidades:
- ✅ Gerenciamento de Moto
- ✅ Cadastro e Listagem de Motos
- ✅ Busca e Filtros Avançados
- ✅ Atualização e Remoção de Motos
- ✅ Sistema de Check-in/Check-out
- ✅ Serviço de Upload de Imagens

---

## 📋 PARTE A: TESTES MANUAIS NO AZURE BOARDS

### PASSO 1: Acessar o Azure DevOps Test Plans

1. **Abra o navegador e acesse:**
   ```
   https://dev.azure.com/Mottu-MS/Mottu-Challenge
   ```

2. **No menu lateral esquerdo, clique em:**
   - `Test Plans` (ícone de lista com check)

3. **Se não houver Test Plans, crie um novo:**
   - Clique no botão `+ New Test Plan`
   - Nome: `Sprint 4 - Compliance, Quality Assurance & Tests`
   - Área: `Mottu-Challenge`
   - Iteration: `Sprint 4`
   - Clique em `Create`

---

### PASSO 2: Criar Test Suites

Dentro do Test Plan criado:

#### Suite 1: Testes Manuais - API

1. **Clique no botão `+` ao lado do nome do Test Plan**
2. Selecione `Static Suite`
3. Nome: `Testes Manuais - Funcionalidades Principais`
4. Clique em `Create`

#### Suite 2: Testes Automatizados

1. **Clique novamente no botão `+`**
2. Selecione `Static Suite`
3. Nome: `Testes Automatizados - API e UI`
4. Clique em `Create`

---

### PASSO 3: Criar Test Cases Manuais

Para cada teste abaixo, siga estes passos:

1. **Clique com botão direito na Suite "Testes Manuais"**
2. Selecione `New Test Case`
3. Preencha os campos conforme o template

---

#### 🧪 TEST CASE 1: Cadastro de Moto

**Informações Básicas:**
- **Título:** `[TC001] Cadastro de Nova Moto`
- **Estado:** `Design`
- **Prioridade:** `1 - Alta`
- **Área:** `Mottu-Challenge`

**Aba "Steps" (Passos):**

```
1. Abrir Postman ou navegador
2. Fazer requisição POST para /api/Motos
3. Enviar JSON:
   {
     "identificador": "MOTO001",
     "ano": 2024,
     "modelo": "Honda CG 160 Titan",
     "placa": "ABC1D23"
   }
4. Verificar resposta
5. Validar status code 201
6. Validar que a moto foi criada
7. Verificar que todos os campos retornaram corretamente
```

**Aba "Summary" (Dados de Entrada):**
```json
{
  "identificador": "MOTO001",
  "ano": 2024,
  "modelo": "Honda CG 160 Titan",
  "placa": "ABC1D23"
}
```

**Expected Result (Resultado Esperado):**
```json
{
  "status": 201,
  "message": "Moto cadastrada com sucesso",
  "data": {
    "id": "auto-generated-id",
    "identificador": "MOTO001",
    "ano": 2024,
    "modelo": "Honda CG 160 Titan",
    "placa": "ABC1D23",
    "disponivel": true
  }
}
```

**Clique em `Save & Close`**

---

#### 🧪 TEST CASE 2: Listar Todas as Motos

**Informações Básicas:**
- **Título:** `[TC002] Listar Todas as Motos`
- **Prioridade:** `2 - Média`

**Steps:**
```
1. Fazer requisição GET para /api/Motos
2. Verificar resposta
3. Validar status code 200
4. Validar que retorna array de motos
5. Verificar estrutura dos dados
```

**Dados de Entrada:**
```
GET /api/Motos
Sem parâmetros
```

**Resultado Esperado:**
```json
{
  "status": 200,
  "data": [
    {
      "id": "...",
      "identificador": "MOTO001",
      "ano": 2024,
      "modelo": "Honda CG 160 Titan",
      "placa": "ABC1D23"
    }
  ]
}
```

---

#### 🧪 TEST CASE 3: Buscar Moto por ID

**Título:** `[TC003] Buscar Moto por ID`

**Steps:**
```
1. Obter ID de uma moto existente
2. Fazer GET /api/Motos/{id}
3. Verificar resposta
4. Validar status 200
5. Validar dados da moto retornada
```

**Dados de Entrada:**
```
GET /api/Motos/{id_valido}
```

**Resultado Esperado:**
```json
{
  "status": 200,
  "data": {
    "id": "{id_valido}",
    "identificador": "MOTO001",
    "ano": 2024,
    "modelo": "Honda CG 160 Titan",
    "placa": "ABC1D23"
  }
}
```

---

#### 🧪 TEST CASE 4: Buscar Moto por Placa

**Título:** `[TC004] Buscar Moto por Placa`

**Steps:**
```
1. Fazer GET /api/Motos?placa=ABC1D23
2. Verificar resposta
3. Validar status 200
4. Validar que retorna exatamente a moto com aquela placa
5. Verificar que não retorna outras motos
```

**Dados de Entrada:**
```
GET /api/Motos?placa=ABC1D23
```

**Resultado Esperado:**
```json
{
  "status": 200,
  "data": {
    "id": "...",
    "placa": "ABC1D23",
    "modelo": "Honda CG 160 Titan",
    "ano": 2024
  }
}
```

---

#### 🧪 TEST CASE 5: Atualizar Placa da Moto

**Título:** `[TC005] Atualizar Placa de Moto`

**Steps:**
```
1. Obter ID de uma moto existente
2. Fazer PUT /api/Motos/{id}
3. Enviar nova placa no body
4. Verificar resposta
5. Validar status 200
6. Fazer GET para confirmar alteração
```

**Dados de Entrada:**
```json
PUT /api/Motos/{id}
{
  "placa": "XYZ9W87"
}
```

**Resultado Esperado:**
```json
{
  "status": 200,
  "message": "Placa atualizada com sucesso"
}
```

---

#### 🧪 TEST CASE 6: Remover Moto

**Título:** `[TC006] Remover Moto da Frota`

**Steps:**
```
1. Criar uma moto de teste
2. Obter o ID
3. Fazer DELETE /api/Motos/{id}
4. Verificar status 200 ou 204
5. Tentar fazer GET para confirmar remoção
6. Validar que retorna 404
```

**Dados de Entrada:**
```
DELETE /api/Motos/{id}
```

**Resultado Esperado:**
```json
{
  "status": 200,
  "message": "Moto removida com sucesso"
}
```

---

#### 🧪 TEST CASE 7: Upload de Imagem

**Título:** `[TC007] Upload de Imagem da Moto`

**Steps:**
```
1. Preparar arquivo de imagem (PNG ou JPG)
2. Fazer POST /api/Motos/checkin
3. Enviar imagem como multipart/form-data
4. Verificar resposta
5. Validar que retorna URL da imagem
6. Verificar que imagem foi salva no storage
```

**Dados de Entrada:**
```
POST /api/Motos/checkin
Content-Type: multipart/form-data

file: [arquivo_imagem.png]
placaMoto: "ABC1D23"
```

**Resultado Esperado:**
```json
{
  "status": 200,
  "message": "Imagem enviada com sucesso",
  "imageUrl": "https://storage.azure.com/..."
}
```

---

#### 🧪 TEST CASE 8: Check-in de Moto

**Título:** `[TC008] Realizar Check-in de Moto`

**Steps:**
```
1. Obter ID de uma moto disponível
2. Fazer POST /api/Motos/checkin
3. Enviar dados do check-in
4. Verificar resposta
5. Validar que moto ficou indisponível
```

**Dados de Entrada:**
```json
POST /api/Motos/checkin
{
  "motoId": "moto-id",
  "entregadorId": "entregador-id",
  "dataCheckin": "2025-10-30T10:00:00Z"
}
```

**Resultado Esperado:**
```json
{
  "status": 200,
  "message": "Check-in realizado com sucesso",
  "checkin": {
    "id": "...",
    "motoId": "...",
    "status": "em_uso"
  }
}
```

---

#### 🧪 TEST CASE 9: Check-out de Moto

**Título:** `[TC009] Realizar Check-out de Moto`

**Steps:**
```
1. Obter ID de uma moto em uso
2. Fazer POST /api/Motos/checkout
3. Enviar dados do check-out
4. Verificar resposta
5. Validar que moto voltou a estar disponível
```

**Dados de Entrada:**
```json
POST /api/Motos/checkout
{
  "checkinId": "checkin-id",
  "dataCheckout": "2025-10-30T18:00:00Z"
}
```

---

#### 🧪 TEST CASE 10: Validação de Placa Única

**Título:** `[TC010] Validar Unicidade de Placa`

**Steps:**
```
1. Cadastrar uma moto com placa ABC1D23
2. Tentar cadastrar outra moto com a mesma placa
3. Verificar que retorna erro 400
4. Validar mensagem de erro apropriada
```

**Dados de Entrada:**
```json
POST /api/Motos
{
  "identificador": "MOTO002",
  "ano": 2024,
  "modelo": "Yamaha Factor 125",
  "placa": "ABC1D23"
}
```

**Resultado Esperado:**
```json
{
  "status": 400,
  "error": "Placa já cadastrada",
  "message": "Já existe uma moto com a placa ABC1D23"
}
```

---

### PASSO 4: Vincular Test Cases às Work Items

Para cada Test Case criado:

1. **Abra o Test Case**
2. **Vá na aba "Links"**
3. **Clique em "+ Add link"**
4. **Selecione "Existing item"**
5. **Link type:** `Tests`
6. **Busque a User Story ou Task correspondente**
   - Por exemplo: "Gerenciamento de Moto" para TC001
   - "Buscar Moto por Placa" para TC004
7. **Clique em "OK"**
8. **Salve o Test Case**

---

## 🤖 PARTE B: TESTES AUTOMATIZADOS

### PASSO 5: Configurar Ambiente Local

#### 5.1 - Instalar Ferramentas

**Node.js e Newman:**
```bash
# 1. Baixe e instale Node.js
# https://nodejs.org/ (versão LTS)

# 2. Abra o terminal e instale Newman
npm install -g newman newman-reporter-html
```

**Python e Selenium:**
```bash
# 1. Baixe e instale Python 3.8+
# https://www.python.org/downloads/

# 2. Crie uma pasta para o projeto
mkdir mottu-tests
cd mottu-tests

# 3. Crie ambiente virtual
python -m venv venv

# 4. Ative o ambiente virtual
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# 5. Instale dependências
pip install selenium webdriver-manager pytest requests
```

---

### PASSO 6: Criar Testes com Postman

#### 6.1 - Importar Collection

1. **Abra o Postman**
2. **Clique em "Import"** (canto superior esquerdo)
3. **Selecione o arquivo `postman_collection.json`** que criei para você
4. **Clique em "Import"**

#### 6.2 - Configurar Environment

1. **No Postman, clique em "Environments"** (menu lateral)
2. **Clique em "+"** para criar novo environment
3. **Nome:** `Mottu-Challenge-Local`
4. **Adicione as variáveis:**

```
VARIABLE          | INITIAL VALUE              | CURRENT VALUE
baseUrl           | http://localhost:5000      | http://localhost:5000
motoId            |                            |
checkinId         |                            |
```

5. **Clique em "Save"**
6. **Selecione este environment** no dropdown no canto superior direito

#### 6.3 - Atualizar URLs na Collection

Para cada request na collection:

1. **Clique no request**
2. **Na URL, substitua** o endereço fixo por: `{{baseUrl}}/api/Motos`
3. **Exemplo:**
   - Antes: `https://api.mottu-challenge.com/api/Motos`
   - Depois: `{{baseUrl}}/api/Motos`

#### 6.4 - Executar Collection

```bash
# No terminal, execute:
newman run postman_collection.json \
  --environment Mottu-Challenge-Local.postman_environment.json \
  --reporters cli,html \
  --reporter-html-export report-api.html
```

---

### PASSO 7: Criar Testes com Selenium

#### 7.1 - Criar Arquivo de Teste

Crie um arquivo `test_mottu_ui.py`:

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

class TestMottu:
    def setup_method(self):
        """Executado antes de cada teste"""
        self.driver = webdriver.Chrome()
        self.driver.maximize_window()
        self.base_url = "http://localhost:5000"  # Ajuste conforme necessário
        
    def teardown_method(self):
        """Executado após cada teste"""
        self.driver.quit()
    
    def test_cadastro_moto(self):
        """Teste de cadastro de moto via interface"""
        driver = self.driver
        driver.get(f"{self.base_url}/motos/cadastro")
        
        # Preencher formulário
        driver.find_element(By.ID, "identificador").send_keys("MOTO001")
        driver.find_element(By.ID, "ano").send_keys("2024")
        driver.find_element(By.ID, "modelo").send_keys("Honda CG 160")
        driver.find_element(By.ID, "placa").send_keys("ABC1D23")
        
        # Submeter
        driver.find_element(By.ID, "btn-salvar").click()
        
        # Verificar sucesso
        wait = WebDriverWait(driver, 10)
        mensagem = wait.until(
            EC.presence_of_element_located((By.CLASS_NAME, "alert-success"))
        )
        assert "sucesso" in mensagem.text.lower()
    
    def test_buscar_moto_placa(self):
        """Teste de busca por placa"""
        driver = self.driver
        driver.get(f"{self.base_url}/motos")
        
        # Buscar
        campo_busca = driver.find_element(By.ID, "busca-placa")
        campo_busca.send_keys("ABC1D23")
        campo_busca.submit()
        
        time.sleep(2)
        
        # Verificar resultado
        resultado = driver.find_element(By.CLASS_NAME, "resultado-busca")
        assert "ABC1D23" in resultado.text
```

#### 7.2 - Executar Testes Selenium

```bash
# Com pytest
pytest test_mottu_ui.py -v

# Com relatório HTML
pytest test_mottu_ui.py --html=report-ui.html --self-contained-html
```

---

### PASSO 8: Criar Test Cases Automatizados no Azure

Para os testes automatizados, crie Test Cases marcados como "Automated":

1. **Na Suite "Testes Automatizados"**
2. **Clique com botão direito → New Test Case**
3. **Preencha:**
   - Título: `[TC-AUTO-001] Cadastro de Moto - API`
   - Automation Status: `Automated`
   - Priority: `1`
4. **Na aba "Associated Automation":**
   - Test Type: `Automated`
   - Automated test name: `TC-AUTO-001_Cadastro_Moto`
5. **Salve**

Repita para todos os 8 testes automatizados.

---

### PASSO 9: Criar Repositório no GitHub

#### 9.1 - Criar Repositório

1. **Acesse:** https://github.com/new
2. **Nome:** `mottu-challenge-tests`
3. **Descrição:** `Testes Sprint 4 - Compliance, QA & Tests`
4. **Visibilidade:** `Public` ✅
5. **Marque:** `Add README file`
6. **Clique em "Create repository"**

#### 9.2 - Clonar e Adicionar Arquivos

```bash
# Clone o repositório
git clone https://github.com/SEU-USUARIO/mottu-challenge-tests.git
cd mottu-challenge-tests

# Copie todos os arquivos que criei para você
# (README.md, postman_collection.json, selenium_tests.py, etc.)

# Adicione ao git
git add .
git commit -m "feat: adiciona testes manuais e automatizados sprint 4"
git push origin main
```

---

### PASSO 10: Gravar Vídeo Demonstrativo

#### 10.1 - Preparação

**Instale OBS Studio:**
- Download: https://obsproject.com/
- Configure resolução: 1920x1080
- FPS: 30

**Prepare o ambiente:**
```bash
# Inicie sua API local
dotnet run

# Em outro terminal, deixe o Postman pronto
# Abra o navegador com Azure DevOps
# Abra VS Code com os códigos
```

#### 10.2 - Roteiro de Gravação (10-12 minutos)

**INTRODUÇÃO (1 min):**
```
"Olá! Vou demonstrar os testes do Sprint 4 do Mottu Challenge.
Vamos ver testes manuais no Azure Boards e testes automatizados
com Postman e Selenium."
```

**AZURE BOARDS (3 min):**
1. Mostre o Test Plan
2. Navegue pelos Test Cases
3. Abra um Test Case e mostre:
   - Dados de entrada
   - Passos
   - Resultado esperado
   - Link com Work Item

**TESTES POSTMAN (3 min):**
1. Abra o Postman
2. Mostre a collection
3. Execute a collection completa
4. Mostre os resultados

**TESTES SELENIUM (2 min):**
1. Mostre o código Python
2. Execute no terminal:
   ```bash
   pytest test_mottu_ui.py -v
   ```
3. Mostre o navegador executando automaticamente

**REPOSITÓRIO GITHUB (1 min):**
1. Abra o repositório
2. Mostre o README
3. Mostre os arquivos de teste

**CONCLUSÃO (1 min):**
```
"Implementamos 10 testes manuais e 16 automatizados,
todos documentados e integrados ao Azure DevOps.
Obrigado!"
```

#### 10.3 - Publicar Vídeo

1. **YouTube:**
   - Faça upload
   - Título: "Sprint 4 - Testes Mottu Challenge"
   - Visibilidade: Não listado
   - Copie o link

2. **Atualize o README:**
   ```markdown
   ## 🎥 Vídeo Demonstrativo
   [Assistir demonstração](https://youtu.be/SEU_VIDEO_ID)
   ```

---

### PASSO 11: Adicionar Professor no Azure DevOps

1. **Acesse:** https://dev.azure.com/Mottu-MS
2. **Clique em "Organization Settings"** (canto inferior esquerdo)
3. **Vá em "Users"**
4. **Clique em "+ Add users"**
5. **Preencha:**
   - Email: email-do-professor@fiap.com
   - Access level: `Basic`
   - Add to projects: `Mottu-Challenge`
   - Roles: `Project Administrator` ou `Contributors`
6. **Clique em "Add"**

---

### PASSO 12: Entrega Final

#### 12.1 - Checklist de Entrega

```
PARTE A - Testes Manuais:
✅ 10 Test Cases criados no Azure Boards
✅ Todos com dados de entrada definidos
✅ Todos com dados de saída esperados
✅ Todos com passos detalhados
✅ Todos vinculados a Work Items

PARTE B - Testes Automatizados:
✅ Collection Postman com 8+ testes
✅ Scripts Selenium com 8+ testes
✅ Repositório GitHub público criado
✅ README com instruções
✅ Vídeo demonstrativo gravado e publicado
✅ Professor adicionado ao Azure DevOps

Documentação:
✅ README.md completo
✅ Guia de configuração
✅ Links para Azure DevOps
✅ Link do vídeo
```

#### 12.2 - Entregar no Sistema

1. **Link do Repositório GitHub**
2. **Link do Vídeo YouTube**
3. **Link do Azure DevOps:**
   ```
   https://dev.azure.com/Mottu-MS/Mottu-Challenge/_testPlans/define
   ```

---

## 🆘 RESOLUÇÃO DE PROBLEMAS

### Problema: "Newman não encontrado"
```bash
# Solução:
npm install -g newman
npm list -g newman  # verificar instalação
```

### Problema: "ChromeDriver incompatível"
```bash
# Solução:
pip install webdriver-manager
```

No código Python, use:
```python
from webdriver_manager.chrome import ChromeDriverManager
driver = webdriver.Chrome(ChromeDriverManager().install())
```

### Problema: "API não responde"
```bash
# Verifique se a API está rodando:
curl http://localhost:5000/api/health

# Ou abra no navegador:
http://localhost:5000/swagger
```

### Problema: "Não consigo criar Test Case no Azure"
- Verifique se tem permissões no projeto
- Vá em Project Settings → Permissions
- Certifique-se de estar no grupo Contributors ou superior

---

## 📞 SUPORTE

**Problemas comuns:**
- API não sobe: verifique .NET SDK instalado
- Testes falhando: verifique URLs e portas
- Azure DevOps: verifique permissões

**Documentação oficial:**
- Azure DevOps: https://docs.microsoft.com/azure/devops/
- Postman: https://learning.postman.com/
- Selenium: https://selenium-python.readthedocs.io/

---



Link do vídeo: [COLOCAR DEPOIS]
