#SIPP=../sipp_ssl
SIPP=../sipp

##############################
# Value Define

# Test Server IP Define
LOCAL_IP  = 100.100.108.141
UAS_LOCAL_PORT = 8120
UAC_LOCAL_PORT = 8200
#TRK_LOCAL_PORT = 8300
TRK_LOCAL_PORT = 5092
DN_LOCAL_PORT = 8100
EPMEM1_PORT   = 8200
EPMEM2_PORT   = 8201
EPMEM3_PORT   = 8202

PBX_IP     = 100.100.106.153
PBX_PORT   = 5060

TRKSVC_IP     = 100.100.106.154
TRKSVC_PORT = 5260

EXTSVC_IP     = 100.100.106.153
EXTSVC_PORT = 5060

EPMEM_NAT_IP     = 100.100.100.100
EPMEM_NAT_PORT   = 5555

# Test Condition Define
CPS        = 2
MAXLINE    = 300
MAXCALLS   = 500
DOD_MAXCALLS   = 3
PAUSE_TIME = 5000

# Test Scenario Define
REG_SCN   = regi.xml
TCPUAC_SCN   = tcp_uac.xml
DNUAC_SCN   = dn_uac.xml
TRKUAC_SCN   = trk_uac.xml
REG_RPORT_SCN   = regi_rport.xml
REG_ROUTE_SCN   = regi_route.xml
UNREG_SCN = unregi.xml
UAC_SCN   = uac.xml
UAC_QUEUE_SCN   = uac_queue.xml
UAC_RPORT_SCN   = uac_rport.xml
UAC_ROUTE_SCN   = uac_route.xml
UAS_SCN   = uas.xml
TRKUAS_SCN   = trk_uas.xml
UAS_REINV_SCN   = uas_reinvite.xml
DODUAS_SCN   = doduas.xml
UAS_RPORT_SCN   = uas_rport.xml
UAS_ROUTE_SCN   = uas_route.xml
UAS_OPT_SCN = uas_opt.xml
UAS_OPTREG_SCN = uas_optreg.xml
UAS_NOTFOUND_SCN = uas_404notfound.xml
OPT_SCN = opt.xml
OPT_RPORT_SCN = opt_rport.xml
OPT_ROUTE_SCN = opt_route.xml

DID_DATA  = uac.csv
DIDNAT_DATA  = uac_nat.csv
DODNAT_DATA  = dod_nat.csv
DOD_DATA  = dod.csv
DN_DATA   = dn.csv
TCPUAC_DATA   = tcp_uac.csv
DNUAC_DATA   = dn_uac.csv
TRKUAC_DATA   = trk_uac.csv
DNNAT_DATA   = dn_nat.csv
OPTNAT_DATA   = opt_nat.csv


# Test DN Define
ANI     = 01012345678
DNIS	= 7100
SDN     = 31001
EDN     = 31600

##############################
# Environment Check
UID     = $(shell id)
ifneq (, $(findstring root, $(UID)))
ROOTCHK = YES
endif

##############################
# Environment Define
PBX_IPPORT   = $(PBX_IP):$(PBX_PORT)
TRKSVC_IPPORT   = $(TRKSVC_IP):$(TRKSVC_PORT)
EXTSVC_IPPORT   = $(EXTSVC_IP):$(EXTSVC_PORT)
UAS_FLAGS  = -sn uas -i $(LOCAL_IP) -p $(UAS_LOCAL_PORT)
TRKUAS_FLAGS  = -sn uas -i $(LOCAL_IP) -p $(TRK_LOCAL_PORT)
DODUAS_FLAGS  = $(PBX_IPPORT) -i $(LOCAL_IP) -p $(EPMEM2_PORT)
UASEPM1_FLAGS  = -sn uas -i $(LOCAL_IP) -p $(EPMEM1_PORT)
UASEPM2_FLAGS  = -sn uas -i $(LOCAL_IP) -p $(EPMEM2_PORT)
UASEPM3_FLAGS  = -sn uas -i $(LOCAL_IP) -p $(EPMEM3_PORT)
UAC_FLAGS  = $(PBX_IPPORT) -i $(LOCAL_IP) -p $(UAC_LOCAL_PORT) #-timeout 100s
TRK_UAC_FLAGS  = $(TRKSVC_IPPORT) -i $(LOCAL_IP) -p $(TRK_LOCAL_PORT) #-timeout 100s
UACEPM1_FLAGS  = $(PBX_IPPORT) -i $(LOCAL_IP) -p $(EPMEM1_PORT)
REG_FLAGS  = $(PBX_IPPORT) -i $(LOCAL_IP) -p $(UAS_LOCAL_PORT)
DN_UAC_FLAGS  = $(EXTSVC_IPPORT) -i $(LOCAL_IP) -p $(DN_LOCAL_PORT)
DN_UAS_FLAGS  = $(EXTSVC_IPPORT) -i $(LOCAL_IP) -p $(UAS_LOCAL_PORT)
OPT_FLAGS  = $(PBX_IPPORT) -i $(LOCAL_IP) -p $(EPMEM1_PORT)
OPTIONS = -max_socket 100 -trace_err -trace_msg -trace_calldebug

CPS_OPT      = -r $(CPS)
PAUSE_OPT    = -d $(PAUSE_TIME)
RTP_ECHO_OPT = # -rtp_echo
MAXLINE_OPT  = -l $(MAXLINE)
MAXCALLS_OPT = -m $(MAXCALLS)
DOD_MAXCALLS_OPT = -m $(DOD_MAXCALLS)

##############################
# Test DN Data Generator
DN_LIST = $(shell seq $(SDN) $(EDN))
DN_CNT  = $(words $(DN_LIST))


uac:
	$(SIPP) $(UAC_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(MAXCALLS_OPT) -sf $(UAC_SCN) -inf $(DID_DATA)
#	$(SIPP) $(UACEPM1_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(MAXCALLS_OPT) -sf $(UAC_QUEUE_SCN) -inf $(DID_DATA)
ifdef ROOTCHK
	#$(SIPP) $(UAC_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(MAXCALLS_OPT) -sf $(UAC_SCN) -inf $(DID_DATA)
else
	$(warning please run with 'sudo make uac')
endif

uac_rport:
	$(SIPP) $(UACEPM1_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) -m 1 -sf $(UAC_RPORT_SCN) -inf $(DIDNAT_DATA)
#	$(SIPP) $(UACEPM1_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(MAXCALLS_OPT) -sf $(UAC_RPORT_SCN) -inf $(DIDNAT_DATA)

uac_route:
	$(SIPP) $(UACEPM1_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) -m 1 -sf $(UAC_ROUTE_SCN) -inf $(DIDNAT_DATA)

trkuas:
	$(SIPP) $(TRKUAS_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT)  -t t1 -sf $(TRKUAS_SCN)

uas:
	$(SIPP) $(UAS_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -t tn -sf $(UAS_SCN)

uas_notfound:
	$(SIPP) $(UAS_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_NOTFOUND_SCN)

uas_reinv:
	$(SIPP) $(UAS_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_REINV_SCN)

uas_rport:
	$(SIPP) $(UAS_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_RPORT_SCN) -inf $(OPTNAT_DATA)

uas_route:
	$(SIPP) $(UASEPM1_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_ROUTE_SCN) -inf $(OPTNAT_DATA)

dod_uas:
	$(SIPP) $(DODUAS_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(DODUAS_SCN)

dod_uas1:
	$(SIPP) $(UASEPM1_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_SCN)

dod_uas2:
	$(SIPP) $(UASEPM2_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_SCN)

dod_uas3:
	$(SIPP) $(UASEPM3_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_SCN)

dod_uas_rport:
	$(SIPP) $(UASEPM1_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_RPORT_SCN) -inf $(OPTNAT_DATA)

dod_uas_route:
	$(SIPP) $(UASEPM1_FLAGS) $(OPTIONS) $(RTP_ECHO_OPT) $(PAUSE_OPT) -sf $(UAS_ROUTE_SCN) -inf $(OPTNAT_DATA)

dod_uac_rport:
	$(SIPP) $(UAC_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(DOD_MAXCALLS_OPT) -sf $(UAC_RPORT_SCN) -inf $(DODNAT_DATA)
#	$(SIPP) $(UAC_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(DOD_MAXCALLS_OPT) -sf $(UAC_RPORT_SCN) -inf $(DIDNAT_DATA)

dod_uac_route:
	$(SIPP) $(UAC_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(DOD_MAXCALLS_OPT) -sf $(UAC_ROUTE_SCN) -inf $(DODNAT_DATA)

tls_regi:
	$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 100 -m 3 -t ln -sf $(REG_SCN) $(PAUSE_OPT) -inf $(DN_DATA)

tcp_regi:
	$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 50 -m 300 -t tn -sf $(REG_SCN) $(PAUSE_OPT) -inf $(DN_DATA)

regi:
	$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 100 -m 3 -t tn -sf $(REG_SCN) $(PAUSE_OPT) -inf $(DN_DATA)

trkuac:
	$(SIPP) $(TRK_UAC_FLAGS) $(OPTIONS) $(CPS_OPT) $(MAXLINE_OPT) $(MAXCALLS_OPT) -t tn -sf $(TRKUAC_SCN) $(PAUSE_OPT) -inf $(TRKUAC_DATA)

dnuac:
	$(SIPP) $(DN_UAC_FLAGS) $(OPTIONS) -r 100 -m 1 -t tn -sf $(DNUAC_SCN) $(PAUSE_OPT) -inf $(DNUAC_DATA)

tcpuac:
	$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 100 -m 1 -t l1 -sf $(TCPUAC_SCN) $(PAUSE_OPT) -inf $(TCPUAC_DATA)

regi_rport:
	$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 100 -m 1 -sf $(REG_RPORT_SCN) -inf $(DNNAT_DATA)

regi_route:
	$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 100 -m 1 -sf $(REG_ROUTE_SCN) -inf $(DNNAT_DATA)

unregi:
	$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 100 -m $(DN_CNT) -sf $(UNREG_SCN) -inf $(DN_DATA)

opt:
	$(SIPP) $(OPT_FLAGS) $(OPTIONS) -r 100 -m 1 -sf $(OPT_SCN) 

opt_rport:
	$(SIPP) $(OPT_FLAGS) $(OPTIONS) -r 100 -m 1 -sf $(OPT_RPORT_SCN) -inf $(OPTNAT_DATA)

opt_route:
	$(SIPP) $(OPT_FLAGS) $(OPTIONS) -r 100 -m 1 -sf $(OPT_ROUTE_SCN) -inf $(OPTNAT_DATA)

uas_opt_epm1:
	$(SIPP) $(UASEPM1_FLAGS) $(OPTIONS) $(PAUSE_OPT) -sf $(UAS_OPT_SCN)

uas_opt_epm2:
	$(SIPP) $(UASEPM2_FLAGS) $(OPTIONS) $(PAUSE_OPT) -sf $(UAS_OPT_SCN)

uas_opt_epm3:
	$(SIPP) $(UASEPM3_FLAGS) $(OPTIONS) $(PAUSE_OPT) -sf $(UAS_OPT_SCN)

uas_optreg_epm1:
	$(SIPP) $(UASEPM1_FLAGS) $(OPTIONS) $(PAUSE_OPT) -sf $(UAS_OPTREG_SCN)

dn:
	@echo "SEQUENTIAL" > $(DN_DATA)
	@$(foreach DN, $(DN_LIST), `echo "$(ANI);$(DN)" >> $(DN_DATA)`)
	@echo "SEQUENTIAL" > $(DID_DATA)
	@echo "$(ANI);$(DNIS)" >> $(DID_DATA)

cleanall:
	@rm -f $(DN_DATA) $(DID_DATA)
	@rm -f *.log

clean:
	@rm -f *.log
