PROJECT(ONCRPC)

CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR})
IF (CMAKE_SIZEOF_VOID_P MATCHES "8")
	ADD_DEFINITIONS(-D_WIN64 -D_X64_)
ELSE()
	ADD_DEFINITIONS(-D_X86_)
ENDIF()

SET(oncrpc_sources 
	librpc/clnt_raw.c 
	librpc/xdr.c 
	librpc/clnt_tcp.c 
	librpc/clnt_udp.c 
	librpc/pmap_rmt.c 
	librpc/rpc_prot.c 
	librpc/svc_autu.c 
	librpc/svc_auth.c 
	librpc/svc_raw.c 
	librpc/svc_run.c 
	librpc/svc_tcp.c 
	librpc/svc_udp.c 
	librpc/xdr_mem.c 
	librpc/xdr_rec.c 
	librpc/auth_non.c 
	librpc/auth_uni.c 
	librpc/authunix.c 
	librpc/bindresv.c 
	librpc/clnt_gen.c 
	librpc/clnt_per.c 
	librpc/clnt_sim.c 
	librpc/get_myad.c 
	librpc/getrpcen.c 
	librpc/getrpcpo.c 
	librpc/pmap_cln.c 
	librpc/pmap_get.c 
	librpc/pmap_gma.c 
	librpc/pmap_pro.c 
	librpc/pmap_pr.c 
	librpc/rpc_call.c 
	librpc/rpc_comm.c 
	librpc/svc_simp.c 
	librpc/xdr_arra.c 
	librpc/xdr_floa.c 
	librpc/xdr_refe.c 
	librpc/xdr_stdi.c 
	librpc/svc.c 
	librpc/bcopy.c 
	librpc/nt.c 
	librpc/oncrpc.def)


ADD_LIBRARY(oncrpc SHARED ${oncrpc_sources})
TARGET_LINK_LIBRARIES(oncrpc wsock32 advapi32)

INSTALL(TARGETS oncrpc
	RUNTIME DESTINATION "bin"
	LIBRARY DESTINATION "lib"
	ARCHIVE DESTINATION "lib")

INSTALL(DIRECTORY "${PROJECT_SOURCE_DIR}/rpc" DESTINATION "include")
