#
# Makefile.am for the Enterprise Management module.
#
#  Licensed to the Apache Software Foundation (ASF) under one
#  or more contributor license agreements.  See the NOTICE file
#  distributed with this work for additional information
#  regarding copyright ownership.  The ASF licenses this file
#  to you under the Apache License, Version 2.0 (the
#  "License"); you may not use this file except in compliance
#  with the License.  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.

include $(top_srcdir)/build/tidy.mk

SUBDIRS = include

AM_CPPFLAGS = \
  $(iocore_include_dirs) \
  -I$(abs_top_srcdir)/lib/records \
  -I$(abs_top_srcdir)/mgmt \
  -I$(abs_top_srcdir)/mgmt/cluster \
  -I$(abs_top_srcdir)/mgmt/utils \
  -I$(abs_top_srcdir)/mgmt/api/include \
  -I$(abs_top_srcdir)/lib \
  $(LIBUNWIND_CFLAGS)

noinst_LTLIBRARIES = libmgmtapilocal.la libmgmtapi.la
lib_LTLIBRARIES = libtsmgmt.la

libmgmtapi_la_SOURCES = \
  CfgContextImpl.cc \
  CfgContextImpl.h \
  CfgContextManager.cc \
  CfgContextManager.h \
  CfgContextUtils.cc \
  CfgContextUtils.h \
  CoreAPI.h \
  CoreAPIShared.cc \
  CoreAPIShared.h \
  EventCallback.cc \
  EventCallback.h \
  GenericParser.cc \
  GenericParser.h \
  INKMgmtAPI.cc \
  NetworkMessage.cc \
  NetworkMessage.h \
  include/mgmtapi.h

if BUILD_TESTS
  noinst_PROGRAMS = traffic_api_cli_remote
endif

libmgmtapilocal_la_SOURCES = \
  CfgContextDefs.h \
  CoreAPI.cc \
  EventControlMain.cc \
  EventControlMain.h \
  NetworkUtilsLocal.cc \
  NetworkUtilsLocal.h \
  TSControlMain.cc \
  TSControlMain.h

libtsmgmt_la_SOURCES = \
  CoreAPIRemote.cc \
  NetworkUtilsRemote.cc \
  NetworkUtilsRemote.h

libmgmtapilocal_la_LIBADD = \
  libmgmtapi.la \
  $(top_builddir)/lib/ts/libtsutil.la

libtsmgmt_la_LDFLAGS = -no-undefined -version-info @TS_LIBTOOL_VERSION@
libtsmgmt_la_LIBADD = @LIBOBJS@ \
  libmgmtapi.la \
  $(top_builddir)/lib/ts/libtsutil.la \
  $(top_builddir)/mgmt/utils/libutils_p.la

if BUILD_TESTS
  traffic_api_cli_remote_SOURCES = APITestCliRemote.cc
endif

traffic_api_cli_remote_LDADD = \
  libtsmgmt.la \
  $(top_builddir)/lib/ts/libtsutil.la \
  @LIBTCL@ @OPENSSL_LIBS@

tidy-local: $(DIST_SOURCES)
	$(CXX_Clang_Tidy)
