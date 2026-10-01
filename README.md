<h1 align="center">certiA1</h1>

<p align="center">
  Instalador e gerenciador de certificados digitais A1 para Windows.
</p>

<p align="center">
  <strong>Versão 2.4.9</strong> · Python · Tkinter · PowerShell · UI Automation
</p>

---

## O que faz

- Lê certificados `.PFX` e `.P12`, valida a senha e apresenta os dados antes da instalação.
- Instala o certificado no repositório pessoal do usuário atual do Windows.
- Permite marcar a chave privada como exportável e habilitar proteção forte.
- Consulta certificados instalados com pesquisa, filtros e ordenação.
- Permite selecionar vários certificados para exclusão, sempre com confirmação.
- Exporta um certificado por vez: como `.PFX` quando há chave privada ou `.CER` sem chave privada.
- Vincula o número de série do certificado ao campo **Certificado** do sistema RenaSoft aberto na tela de CT-e ou MDF-e.

## Requisitos

- Para usar o executável: Windows 10 ou posterior e PowerShell disponível. Não é necessário instalar Python no computador do cliente.
- Para executar o código-fonte ou gerar o executável: Python e as dependências de [requirements.txt](requirements.txt).
- O executável x86 requer Windows de 32 bits; o x64 requer Windows de 64 bits. Windows x64 também executa aplicativos x86.

## Usar o aplicativo

1. Abra o certiA1 e escolha um arquivo `.PFX` ou `.P12`.
2. Informe a senha. Depois da validação, confira os dados no popup e selecione **Confirmar dados**.
3. Revise as opções e escolha **Instalar certificado**.
4. Para gerenciar certificados, abra **Certificados instalados**. Use Ctrl ou Shift para selecionar mais de um ao excluir.

### Vincular ao sistema RenaSoft

1. Abra **Configuração do Sistema** no RenaSoft e navegue manualmente até a página de CT-e ou MDF-e desejada.
2. No certiA1, confirme os dados do certificado e clique em **Vincular nesta tela**, ou abra **Certificados instalados**, selecione uma única linha e clique em **Vincular ao sistema**.
3. O aplicativo localiza o campo **Certificado**, entra no modo **Alterar F2** se necessário e preenche o número de série.
4. Confira o valor e salve no próprio RenaSoft.

O certiA1 não navega pelo menu lateral do RenaSoft nem salva as configurações por você. Se não encontrar exatamente um campo correspondente, interrompe a ação sem preencher outro campo.

## Executar pelo código

No Prompt de Comando do Windows:

```bat
python -m venv .venv
.venv\Scripts\activate.bat
build_exe.bat
```

O script gera a versão x64 e, se houver um Python de 32 bits instalado e reconhecido pelo Python Launcher, também gera a versão x86. Cada arquitetura usa seu próprio ambiente virtual e instala as dependências de `requirements.txt`.
O PyInstaller empacota o interpretador Python e as dependências dentro de cada executável; distribua o arquivo `.exe` correspondente à arquitetura do Windows do cliente. O Python instalado na máquina de build não é necessário no computador de destino.

```text
dist\CertiA1 Instalador 2.4.9 x64.exe
dist\CertiA1 Instalador 2.4.9 x32.exe  (quando Python de 32 bits estiver instalado)
```

Para gerar as duas versões, instale Pythons de 64 e 32 bits compatíveis com as dependências do projeto. O script informa quando não encontrar o runtime x86.

Para executar sem compilar, com o ambiente virtual ativo:

```bat
python -m pip install -r requirements.txt
python main.py
```

## Segurança e dados

- A senha do certificado é usada durante a operação e não é salva pelo aplicativo.
- A instalação e a consulta usam o repositório pessoal do Windows (`Cert:\CurrentUser\My`).
- Arquivos `.PFX` exportados são protegidos com a senha definida no momento da exportação.
- A automação do RenaSoft preenche o campo, mas deixa a revisão e o salvamento final para o usuário.

## Arquivos de marca

- `certia1.ico`: ícone da janela e do executável.
- `certia1-brand.png`: marca exibida na barra lateral.
