!include <ntwin32.mak>

# If the rpc include directory is not included in the standard path
# you have to give the path to it here.
RPCINCLUDEPATH = ..

# If the rpc library is not included in the standard lib path
# you have to give the path to it here.
RPCLIBPATH = ..\bin\\

all: portmap.exe inst_pm.exe portmap.srg

# Update the object file if necessary

clean:
    del *.obj *.exe

portmapd.res:  portmapd.rc servregids.h
    $(rc) portmapd.rc

portmap.res:   portmap.rc
    $(rc) portmap.rc

portmap.srg:	portmapd.res servreg.obj
#    $(link) -Tpd $(LD_FLAGS) c0d32.obj \
#    servreg.obj,portmap.srg,,import32.lib cw32.lib,portmapd.def,portmapd.res
#    copy portmap.srg ..\bin

portmap.exe: service.obj portmap.obj servregi.obj $(RPCLIBPATH)oncrpc.lib
    $(link) $(ldebug) $(conflags) -out:portmap.exe portmap.obj service.obj servregi.obj $(conlibs) $(RPCLIBPATH)oncrpc.lib wsock32.lib  advapi32.lib user32.lib
    copy portmap.exe ..\bin

inst_pm.exe: inst_pm.obj
    $(link) $(ldebug) $(conflags) -out:inst_pm.exe inst_pm.obj $(conlibs) advapi32.lib
    copy inst_pm.exe ..\bin

.c.obj:
    $(cc) /I$(RPCINCLUDEPATH) $(cdebug) $(cflags) $(cvars) $*.c
