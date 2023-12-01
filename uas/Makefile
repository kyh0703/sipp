SIPP=../build/bin/sipp

REGI_SCENARIO_PATH = xml/register
CALL_SCENARIO_PATH = xml/call
DATA_PATH          = csv
LOG_PATH           = log

PBX         = 100.100.106.153:5060
LOCAL_IP    = 100.100.108.141
LOCAL_PORT  = 8120

PAUSE_TIME  = 1000
OPTIONS     = -max_socket 100 -trace_err -trace_msg -trace_calldebug

START_DN    = 6001
END_DN      = 6300
MD5_ID      = test
MD5_PSW     = test

defeault: dn register base

.PHONY: dn
dn:
	@echo "dn:"
	@echo "SEQUENTIAL" > $(DATA_PATH)/dn.csv
	@echo "# user, domain, authentication" >> $(DATA_PATH)/dn.csv
	@$(foreach DN, \
		 $(shell seq $(START_DN) $(END_DN)), \
		 `echo "$(DN);$(PBX);[authentication username=$(MD5_ID) password=$(MD5_PSW)]" >> $(DATA_PATH)/dn.csv` \
	 )

regist:
	@echo "regist:"
	@$(SIPP) $(OPTIONS) \
		-i $(LOCAL_IP) -p $(LOCAL_PORT) \
		-d $(PAUSE_TIME) \
		-r 100 -m 3 -t tn \
		-max_socket 100 -trace_err -trace_msg \
		-sf $(REGI_SCENARIO_PATH)/register.xml \
		-inf csv/dn.csv

.PHONY: unregist
unregist:
	@echo "unregist:"
	@$(SIPP) $(OPTIONS) \
		-i $(LOCAL_IP) -p $(LOCAL_PORT) \
		-d $(PAUSE_TIME) \
		-r 100 -m 3 -t tn \
		-max_socket 100 -trace_err -trace_msg \
		-sf $(REGI_SCENARIO_PATH)/unregister.xml \
		-inf csv/dn.csv

.PHONY: base
base:
	@echo "base:"
	@$(SIPP) $(OPTIONS) \
		-sn uas \
		-i $(LOCAL_IP) -p $(LOCAL_PORT) \
		-d $(PAUSE_TIME) \
		-t tn \
		-sf $(SCENARIO_PATH)/base.xml

.PHONY: base_echo
base_rtpecho:
	@echo "base_echo:"
	@$(SIPP) $(OPTIONS) \
		-sn uas \
		-i $(LOCAL_IP) -p $(LOCAL_PORT) \
		-d $(PAUSE_TIME) \
		-rtp-echo -t tn \
		-sf $(SCENARIO_PATH)/base.xml

clean:
	@rm -f *.log
