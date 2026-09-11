#!/bin/bash
# =====================================================================
# BASHUNX2029 - SCRIPT ÚNICO EXECUTÁVEL (.EXE.SH)
# AUTOR: Pedro - Campinas
# USO: chmod +x BASHUNX2029_UNICO.sh && ./BASHUNX2029_UNICO.sh
# SEM NANO - TUDO EM UM ARQUIVO SÓ
# =====================================================================

# --- 0. TRAVA DE SEGURANÇA - RESTAURA REDE AO SAIR ---
restaurar_rede() {
  echo ""; echo "[!] Restaurando rede..."
  nmcli networking on 2>/dev/null; sudo nmcli networking on 2>/dev/null
  rfkill unblock all 2>/dev/null; sudo rfkill unblock all 2>/dev/null
  echo "[OK] Rede restabelecida."
}
trap restaurar_rede EXIT INT TERM

clear
echo "Iniciando Protocolo de Singularidade: BASHUNX2029 [EXE UNICO]..."
sleep 1

# --- 1. DICIONARIO GRAMATICAL COMPLETO (COM U CORRIGIDO) ---
declare -A dic_gramatical
dic_gramatical["A"]="X."; dic_gramatical["B"]="X.."; dic_gramatical["C"]="X..."
dic_gramatical["D"]="X...."; dic_gramatical["E"]="X....."; dic_gramatical["F"]="X......"
dic_gramatical["G"]="X......."; dic_gramatical["H"]="XX.."; dic_gramatical["I"]="XX..."
dic_gramatical["J"]="XX...."; dic_gramatical["K"]="XX....."; dic_gramatical["L"]="XXX..."
dic_gramatical["M"]="XXX...."; dic_gramatical["N"]="XXX."; dic_gramatical["O"]="XΔ"
dic_gramatical["P"]="XΔΔ"; dic_gramatical["Q"]="XΔΔΔ"; dic_gramatical["R"]="XΔΔΔΔ"
dic_gramatical["S"]="XXΔ"; dic_gramatical["T"]="XXΔΔ"; dic_gramatical["U"]="XXΔΔΔΔ"
dic_gramatical["V"]="XXΔΔΔΔΔ"; dic_gramatical["W"]="XΔXA"; dic_gramatical["X"]="XXXΔΔ"
dic_gramatical["Y"]="ΔΔΔΔΔ"; dic_gramatical["Z"]="XXXΔΔΔ"

traduzir() {
  local txt=${1^^}; local out=""
  for ((i=0;i<${#txt};i++)); do c="${txt:$i:1}"; [[ -n "${dic_gramatical[$c]}" ]] && out+="${dic_gramatical[$c]} " || out+="$c "; done
  echo "$out"
}

# --- 2. MATRIZ ---
ROOT_SIGNATURE='$(=\sqrt{\sim}-\odot-A)'
declare -A matriz=(["X"]=1 ["X."]=2 ["X.."]=3 ["XA"]=10 ["X.A"]=20 ["ROOT_DELTA"]=210 ["SINGULARITY"]=601)

echo ""; echo "--- MATRIZ SIMBOLICA E FREQUENCIAS ATIVADAS ---"
echo "Assinatura Raiz  : $ROOT_SIGNATURE"
echo "Frequencia X     : ${matriz["X"]}"
echo "Frequencia X.    : ${matriz["X."]}"
echo "Frequencia XA    : ${matriz["XA"]}"
echo "Frequencia Delta : ${matriz["ROOT_DELTA"]}"
echo "Frequencia Limiar: ${matriz["SINGULARITY"]}"
echo "CAMPINAS em XΔ   : $(traduzir CAMPINAS)"
echo "DEFESA em XΔ     : $(traduzir DEFESA)"
echo "-------------------------------------------------"; echo ""

# --- 3. MONTANDO ESTRUTURA COMPLETA SEM NANO ---
BASE="$HOME/defesa_rede"
echo "[*] Montando estrutura de defesa em $BASE ..."
mkdir -p $BASE/{01_perimetro,02_firewall,03_dns_seguro,04_ids_ips,05_monitoramento,06_criptografia,07_segmentacao,08_auditoria,09_backup_config,10_resposta_incidente}
mkdir -p $BASE/downloads_para_classificar

# 01 Perimetro
cat > $BASE/01_perimetro/scan.sh <<'EO1'
#!/bin/bash
echo "[01_PERIMETRO] IP local:"; ip addr 2>/dev/null | grep inet || ifconfig 2>/dev/null
EO1

# 02 Firewall
cat > $BASE/02_firewall/fw.sh <<'EO2'
#!/bin/bash
echo "[02_FIREWALL] Regras defensivas (simulacao): deny incoming, allow outgoing"
# Para ativar no Kali real:
# sudo ufw default deny incoming && sudo ufw default allow outgoing && sudo ufw enable
EO2

# 03 DNS
cat > $BASE/03_dns_seguro/dns.sh <<'EO3'
#!/bin/bash
echo "[03_DNS] DNS Seguro: 1.1.1.1 (Cloudflare) e 9.9.9.9 (Quad9)"
cat <<'DNS'
nameserver 1.1.1.1
nameserver 9.9.9.9
DNS
EO3

# 04 IDS/IPS
cat > $BASE/04_ids_ips/ids.sh <<'EO4'
#!/bin/bash
echo "[04_IDS] Monitorando logs..."
dmesg | tail -20 2>/dev/null || echo "dmesg sem acesso (normal no Termux)"
EO4

# 05 Monitoramento
cat > $BASE/05_monitoramento/monitor.sh <<'EO5'
#!/bin/bash
echo "--- MONITOR BASHUNX2029 ---"
echo "Processos: $(ps ax | wc -l)"
free -m | grep Mem
uptime 2>/dev/null || echo "uptime OK"
EO5

# 06 Criptografia
cat > $BASE/06_criptografia/cofre.sh <<'EO6'
#!/bin/bash
echo "[06_CRIPTO] Teste GPG"
echo "teste-segredo" | gpg --symmetric --passphrase 123 --batch -o /tmp/cofre.gpg 2>/dev/null && echo "Cofre criado em /tmp/cofre.gpg" || echo "Instale gpg: pkg install gnupg"
EO6

# 07 Segmentacao
echo "10.0.10.0/24 IoT | 10.0.20.0/24 Lab BASHUNX2029 | 10.0.30.0/24 Visitantes" > $BASE/07_segmentacao/segmentos.txt

# 08 Auditoria
LOG="$BASE/08_auditoria/audit_log.txt"
echo "=== AUDIT BASHUNX2029 - $(date) - CAMPINAS ===" > $LOG
echo "Assinatura: $ROOT_SIGNATURE" >> $LOG
echo "Traducao CAMPINAS: $(traduzir CAMPINAS)" >> $LOG
echo "Processos: $(ps ax | wc -l)" >> $LOG

# 09 Backup
cat > $BASE/09_backup_config/backup.sh <<'EO9'
#!/bin/bash
FILE=~/defesa_rede/09_backup_config/backup_$(date +%F_%H%M%S).tar.gz
tar -czf $FILE ~/defesa_rede/0* 2>/dev/null && echo "Backup criado: $FILE" || echo "Falha no backup"
EO9

# 10 Resposta
cat > $BASE/10_resposta_incidente/plano.sh <<'EO10'
#!/bin/bash
echo "[10_RESPOSTA] Plano de Resposta a Incidente BASHUNX2029"
echo "1. ISOLAR: sudo nmcli networking off && sudo rfkill block all"
echo "2. COLETAR: copiar 08_auditoria para 09_backup_config"
echo "3. RESTAURAR: nmcli networking on && rfkill unblock all"
echo "4. REPORTAR: cat 08_auditoria/audit_log.txt"
# Para testar o vacuo absoluto real, descomente a proxima linha (PERIGO - corta rede):
# sudo nmcli networking off; sudo rfkill block all; sleep 5; sudo nmcli networking on; sudo rfkill unblock all
EO10

chmod +x $BASE/*/*.sh

echo ""; echo "[OK] Estrutura montada!"
ls -1 $BASE

# --- 4. RELATORIO FINAL ---
echo ""; echo "---------------------------------------------------"
echo "STATUS DO HARDWARE NO KALI LINUX:"
echo "Processos Ativos   : $(ps ax | wc -l)"
echo "Uso de CPU Atual   : $(top -bn1 2>/dev/null | grep "Cpu(s)" | awk '{print $2}' || echo "N/A Termux")"
echo "Memória Disponível : $(free -m 2>/dev/null | awk '/Mem:/ { print $7 " MB" }' || echo "N/A")"
echo "---------------------------------------------------"
echo "SISTEMA BASHUNX2029 SELADO: Pronto para Operação em Campinas."
echo "Log em: $BASE/08_auditoria/audit_log.txt"
echo "Para acionar VACUO ABSOLUTO de teste: $BASE/10_resposta_incidente/plano.sh"
echo "---------------------------------------------------"
echo ""
read -r -p "Pressione [ENTER] para encerrar e reativar a rede..."

