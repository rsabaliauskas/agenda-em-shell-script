# 📅 Script de Agenda de Compromissos

## 🎯 Objetivo deste Script
Este é um script simples e rápido para avisos de compromissos. Ao ser executado, ele mostra os compromissos agendados para o dia corrente e também os agendados para os dias à frente. Além disso, também emite um lembrete baseado na hora do compromisso. 

A quantidade de dias dessa antevisão dos compromissos à frente pode ser definida facilmente (linha: `DiasDosLembretes=7`).

### Histórico de Versões
*   **Em relação ao "agenda 3.x":** Foi acrescentada a possibilidade de lembretes através de uma caixa gráfica (`dialog`) ou através de uma música no horário do compromisso.
*   **Em relação ao "agenda 4.X":** Houve uma simplificação geral do funcionamento, eliminando diretórios e resumindo tudo a dois arquivos (`agenda.sh` e `agenda.txt`). Também houve o acréscimo da possibilidade de marcar compromissos por dia da semana ou para todos os anos, meses ou dias.
*   **Versão 5.3:** Simplificação do "MENU PRINCIPAL", agora com apenas duas opções.
*   **Versão 5.4:** Limpeza geral do código.

---

## ℹ️ Informações Gerais

*   **Versão:** 5.4 (19/08/2016)
*   **Autor:** Ricardo Sabaliauskas (<rsabaliauskas@gmail.com>)
*   **Licença:** GPL (O uso é de sua total responsabilidade)

### 🛠️ Dependências
Subentende-se que é necessário o **Bash** em uma versão recente, além de:

1.  **Editor de Texto:** A ser definido conforme a disponibilidade do seu sistema ou de sua preferência (configurável na linha `Editor=kate` no script `agenda.sh`).
2.  **Pacotes do Sistema:**
    *   `dialog`
    *   `Konsole` (É o padrão, mas você pode configurar o `gnome-terminal` ou outro console gráfico editando a linha `Terminal="konsole --noclose -e"`, lembrando de incluir o parâmetro para executar comandos).

---

## 🚀 1.0) Preparação

Trata-se de um "avisador" ou agenda de compromissos para quem usa muito o computador. Seu uso padrão fará com que um aviso com os compromissos de todo o dia (mais uma antevisão configurável de 7 dias) apareça na inicialização do ambiente gráfico. 

Ele também pode ser usado em ambientes sem modo gráfico. O segundo aviso baseado em horários pode ser uma tela gráfica (`dialog`), um aviso sonoro (MP3) ou ambos. A vantagem sobre ferramentas como *Evolution* ou *Korganizer* é a rapidez de agendamento e o aprendizado ágil. 

Permite também o uso de parâmetros. Exemplo: se você quiser apenas agendar e não precisar ver nenhum compromisso, execute:
```bash
bash agenda.sh 1
```

### 1º Passo: Permissões de Execução
Dê permissão de execução ao script. Supondo que você já está dentro do diretório onde o arquivo `agenda.sh` está presente, execute no terminal:

```bash
chmod +x agenda.sh
```

### 2º Passo: Configuração Interna
Você pode colocar o script em qualquer lugar, mas caso não esteja acostumado com o Linux, recomendo colocá-lo dentro do seu diretório `home` (`/home/$USER`). Este é o local padrão onde os gerenciadores de arquivos (como *Nautilus* ou *Konqueror*) abrem.

Se executado na `home`, você não precisará mudar nenhuma variável inicialmente. Caso mude de diretório e precise ajustar o local explicitamente, procure e edite a linha abaixo:

```bash
LocalizacaoDoScript="/home/$USER"
```
*Nota: Se o caminho do seu diretório contiver espaços vazios, é obrigatório o uso de aspas:*
```bash
LocalizacaoDoScript="/home/eu/Agenda de Compromissos"
```

### 3º Passo: Inicialização no seu Ambiente Gráfico
Para que o script cumpra seu papel, configure-o para iniciar junto com o sistema. O exemplo abaixo aborda o ambiente **KDE 3.5.10 / 4.x**:

No **KDE**, abra um editor de texto e cole as linhas abaixo:

```bash
#!/bin/bash

# Iniciar o Cronometro:
bash /home/$USER/agenda.sh 0 &

# Alertar os horários dos compromissos através do dialog:
konsole -e bash /home/$USER/agenda.sh &
```
*Nota: Ajuste o caminho `/home/$USER/agenda.sh` caso tenha salvo o script em outro local.*

Salve o arquivo com o nome `autostart.sh`, dê permissão de execução e mova-o para a pasta de inicialização do KDE:

```bash
chmod +x autostart.sh
mv autostart.sh /home/$USER/.kde/Autostart
```

---

## ⚙️ 2.0) Funcionamento

Diferente de ferramentas complexas, o agendamento aqui é instantâneo. Ao executar o comando `bash agenda.sh`, a seguinte interface será exibida no terminal:

```text
        julho 2010           agosto 2010          setembro 2010
   Do Se Te Qu Qu Se Sá  Do Se Te Qu Qu Se Sá  Do Se Te Qu Qu Se Sá
                1  2  3   1  2  3  4  5  6  7            1  2  3  4
    4  5  6  7  8  9 10   8  9 10 11 12 13 14   5  6  7  8  9 10 11
   11 12 13 14 15 16 17  15 16 17 18 19 20 21  12 13 14 15 16 17 18
   18 19 20 21 22 23 24  22 23 24 25 26 27 28  19 20 21 22 23 24 25
   25 26 27 28 29 30 31  29 30 31              26 27 28 29 30

   ================================================================
   ***   COMPROMISSOS  DE HOJE   ****   24-Ago-2010 Ter 13:23   ***
   14:00 -> Dentista
   ================================================================
   ***   COMPROMISSOS  FUTUROS   ****   P/ os próximos 7 dias   ***
   Para daqui a 1 dias:
```
