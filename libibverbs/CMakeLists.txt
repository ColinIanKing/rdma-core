publish_headers(infiniband
  arch.h
  driver.h
  kern-abi.h
  marshall.h
  opcode.h
  sa-kern-abi.h
  sa.h
  verbs.h
  )

if (NOT NL_KIND EQUAL 0)
  set(NEIGH "neigh.c")
else()
  set(NEIGH "")
endif()

rdma_library(ibverbs libibverbs.map
  # See Documentation/versioning.md
  1 1.3.${PACKAGE_VERSION}
  cmd.c
  compat-1_0.c
  device.c
  enum_strs.c
  init.c
  marshall.c
  memory.c
  ${NEIGH}
  sysfs.c
  verbs.c
  )
target_link_libraries(ibverbs LINK_PRIVATE
  ${NL_LIBRARIES}
  ${CMAKE_THREAD_LIBS_INIT}
  ${CMAKE_DL_LIBS}
  )
