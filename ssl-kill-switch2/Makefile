ARCHS := armv7
#arm64

# include /opt/theos/makefiles/common.mk
include ~/theos/makefiles/common.mk

TWEAK_NAME = SSLKillSwitch2
SSLKillSwitch2_FILES = SSLKillSwitch/SSLKillSwitch.m SSLKillSwitch/HTTPParser.m
SSLKillSwitch2_LIBRARIES = MobileGestalt lockdown System
SSLKillSwitch2_FRAMEWORKS = Security CFNetwork Foundation CoreFoundation CoreTelephony IOKit
#SSLKillSwitch2_PRIVATE_FRAMEWORKS=XPCKit

# Build as a Substrate Tweak
SSLKillSwitch2_CFLAGS=-DSUBSTRATE_BUILD
#SSLKillSwitch2_LDFLAGS=-lxpc –dylib1.o

include $(THEOS_MAKE_PATH)/tweak.mk
include $(THEOS_MAKE_PATH)/aggregate.mk

#IPHONEADDR=192.168.12.249
#IPHONEADDR=192.168.0.144
IPHONEADDR=192.168.1.69

doclean:
	rm -f packages/com.nablac0d3.SSLKillSwitch2_0.10-*+debug_iphoneos-arm.deb

doall: doclean clean all package
	mv packages/com.nablac0d3.SSLKillSwitch2_0.10-*+debug_iphoneos-arm.deb packages/com.nablac0d3.SSLKillSwitch2.deb
	sshpass -p alpine scp packages/com.nablac0d3.SSLKillSwitch2.deb root@$(IPHONEADDR):/var/root
	sshpass -p alpine ssh root@$(IPHONEADDR)

ondeviceconsole:
	sshpass -p alpine ssh root@$(IPHONEADDR) ondeviceconsole

shell:
	sshpass -p alpine ssh root@$(IPHONEADDR)

after-install::
	# Respring the device
	install.exec "killall -9 SpringBoard"
