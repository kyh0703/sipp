SIPP=../build/bin/sipp

#DN_LIST = $(shell seq $(SDN) $(EDN))
#DN_CNT  = $(words $(DN_LIST))

REGI_SCENARIO_PATH = xml/register
CALL_SCENARIO_PATH = xml/call
DATA_PATH          = csv

PBX         = 100.100.106.153:5060
LOCAL_IP    = 100.100.108.141
LOCAL_PORT  = 8120

PAUSE_TIME  = 1000
OPTIONS     = -max_socket 100 -trace_err -trace_msg -trace_calldebug

START_DN    = 6001
END_DN      = 6300

defeault: data register base

.PHONY: data
data:
	@echo "data:"
	@echo "SEQUENTIAL" > $(DATA_PATH)/dn.csv
	@$(foreach DN, $(shell seq $(START_DN) $(END_DN)), `echo "$(DN)" >> $(DATA_PATH)/dn.csv`)

register:
	@echo "register:"
	@$(SIPP) $(OPTIONS) \
 		$(PBX) \
		-i $(LOCAL_IP) -p $(LOCAL_PORT) \
		-d $(PAUSE_TIME) \
		-r 100 -m 3 -t tn \
		-sf $(REGI_SCENARIO_PATH)/register.xml \
		-inf csv/dn.csv

.PHONY: unregister
unregister:
	@echo "unregister:"
	@$(SIPP) $(OPTIONS) \
		$(PBX) \
		-d $(PAUSE_TIME) \
		-r 100 -m 3 -t tn \
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
