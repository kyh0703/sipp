SIPP=../build/bin/sipp

DATA_PATH     = csv
SCENARIO_PATH = xml

PBX        = 100.100.106.143:5070
LOCAL_IP   = 100.100.108.141
LOCAL_PORT = 8200

CPS         = 1
MAX_LINE    = 300
MAX_CALL    = 1
PAUSE_TIME  = 5000

default: uac

.PHONY: uac
uac:
	$(SIPP) \
		$(PBX) -i $(LOCAL_IP) -p $(LOCAL_PORT) \
		-max_socket 100 \
		-t un \
		-r $(CPS) \
		-l $(MAX_LINE) \
		-m $(MAX_CALL) \
		-sf $(SCENARIO_PATH)/uac.xml \
		-inf $(DATA_PATH)/uac.csv

.PHONY: clean
clean:
	@rm -f *.log
