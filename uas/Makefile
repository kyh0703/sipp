SIPP=../bin/sipp

DN_LIST = $(shell seq $(SDN) $(EDN))
DN_CNT  = $(words $(DN_LIST))

SCENARIO_PATH = xml/scenario
DATA_PATH     = csv

PBX         = 100.100.106.153:5060
LOCAL_IP    = 100.100.108.141
LOCAL_PORT  = 8120

PAUSE_TIME  = 1000
OPTIONS     = -max_socket 100 -trace_err -trace_msg -trace_calldebug

START_DN    = 6001
END_DN      = 6300

defeault: register base


.PHONY: show
show:
	@echo "show:"	
	#@echo "SEQUENTIAL" > $(DN_DATA)
	#@$(foreach DN, $(DN_LIST), `echo "$(ANI);$(DN)" >> $(DN_DATA)`)
	#@echo "SEQUENTIAL" > $(DID_DATA)
	#@echo "$(ANI);$(DNIS)" >> $(DID_DATA)

.PHONY: data
data:
	@echo "data:"
	

.PHONY: register
register:
	@echo "register:"
	@$(SIPP) $(OPTIONS) \
 		$(PBX) \
		-i $(LOCAL_IP) -p $(LOCAL_PORT) \
		-d $(PAUSE_TIME) \
		-r 100 -m 3 -t tn \
		-sf $(SCENARIO_PATH)/register.xml \
		-inf csv/dn.csv

.PHONY: unregister
unregister:
	@echo "unregister:"
	@$(SIPP) $(REG_FLAGS) $(OPTIONS) -r 100 -m $(DN_CNT) -sf $(UNREG_SCN) -inf $(DN_DATA)

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
