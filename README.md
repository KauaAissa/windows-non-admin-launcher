## 📘 Explicação

`__COMPAT_LAYER` é uma variável especial do Windows que permite configurar modos de compatibilidade para execução de programas.

Ao definir `RunAsInvoker`, o Windows ignora o manifesto do executável (mesmo que ele peça `requireAdministrator`) e executa o programa com os mesmos privilégios do processo pai.

Isso faz com que **nenhum prompt do UAC apareça**, desde que o próprio `.bat` também **não seja executado como administrador**.

Além disso, é importante **salvar o arquivo `.bat` com codificação ANSI**. Arquivos `.bat` salvos em UTF-8 com BOM, por exemplo, podem causar problemas na execução ou exibir caracteres inesperados.  
A codificação ANSI garante compatibilidade com o interpretador de comandos do Windows, especialmente quando não há necessidade de caracteres especiais fora do padrão ASCII.

> 💡 Em editores como o Notepad++ ou VS Code, é possível alterar a codificação facilmente antes de salvar o arquivo.

---

## ⚠️ Observações importantes

- Em alguns Programas que exigem privilégios de administrador podem **não funcionar corretamente** ao serem iniciados dessa forma.
- Esse método **não fornece privilégios de administrador**, ele apenas evita que o UAC solicite elevação.
- Pode ser útil para rodar softwares em ambientes restritos, ou quando se sabe que o programa não precisa realmente de privilégios para executar suas funções principais.

---

## ✅ Exemplos de uso

- Automatizar testes ou execuções com ferramentas que normalmente pedem elevação.
- Evitar prompts do UAC em scripts de desenvolvimento.
- Executar programas em ambientes corporativos com restrições de privilégio.

---

## 💻 Código `.bat` de exemplo e como executar

1. Crie uma pasta e, dentro dela, crie um arquivo de texto (usando o Bloco de Notas, por exemplo).
2. Adicione o seguinte conteúdo no arquivo:

```bat
@echo off
:: Evita que o Windows solicite privilégios elevados (UAC), mesmo que o executável peça
set __COMPAT_LAYER=RunAsInvoker

:: Substitua as aspas pelo nome do programa .exe desejado (o arquivo precisa estar na mesma pasta)
start "Nome da instalação .exe"
```

- Substitua "Nome da instalação .exe" pelo nome real do arquivo .exe que deseja executar.
- Salve o arquivo com a extensão .bat, selecione a codificação ANSI e salve dentro da mesma pasta onde está o arquivo .exe.
- Após o arquivo estar salvo na mesma pasta, execute o .bat criado.

## 📂 Restrição de instalação

⚠️ **Atenção:** não é possível realizar a instalação de arquivos `.exe` diretamente no diretório `C:\Program Files`.  
Esse método só funciona corretamente quando o instalador `.exe` grava **todos os seus componentes** dentro do diretório do **usuário** (por exemplo: `C:\Users\SeuUsuario\AppData\Local` ou qualquer outra pasta pessoal).

Se durante a instalação o programa tentar salvar arquivos no `Program Files`, a execução falhará, pois esse diretório exige privilégios administrativos.  
Ou seja: o `RunAsInvoker` só é útil quando o instalador permite que os arquivos sejam colocados em pastas do usuário, e não quando força a escrita em diretórios do sistema.

---

## 📖 Artigo completo

Se quiser entender mais a fundo sobre essa técnica, seus riscos e como proteger ambientes corporativos e escolares contra esse tipo de prática, acesse meu artigo no Medium:

🔗 [Como proteger ambientes corporativos e escolares contra scripts RunAsInvoker](https://medium.com/@kaua.aissa.dev/como-proteger-ambientes-corporativos-e-escolares-contra-scripts-runasinvoker-a11fb4daaeca)

---

## 📌 Autor

Desenvolvido por **Kauã Aissa** 💻
<img src="assets/blackcat.png" alt="Logo Gato Preto" width="120" align="right" />

🔗 [LinkedIn](https://www.linkedin.com/in/kauaaissa)  
🔗 [GitHub](https://github.com/KauaAissa)

---
