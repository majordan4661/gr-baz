# Copyright 2011 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
# Install public header files
########################################################################
install(FILES
    baz_print_char.h
	baz_unpacked_to_packed_bb.h
	baz_pow_cc.h
	baz_delay.h
	baz_puncture_bb.h
	baz_depuncture_ff.h
	baz_swap_ff.h
	baz_agc_cc.h
	baz_test_counter_cc.h
	baz_rtl_source_c.h
    DESTINATION include/baz
)

########################################################################
# Setup library
########################################################################
include(GrPlatform) #define LIB_SUFFIX

add_library(gnuradio-baz SHARED
	baz_print_char.cc
	baz_unpacked_to_packed_bb.cc
	baz_pow_cc.cc
	baz_delay.cc
	baz_puncture_bb.cc
	baz_depuncture_ff.cc
	baz_swap_ff.cc
	baz_agc_cc.cc
	baz_test_counter_cc.cc
	baz_rtl_source_c.cc
	rtl2832.cc
	rtl2832-tuner_e4000.cc
	rtl2832-tuner_fc0013.cc
	rtl2832-tuner_fc0012.cc
	rtl2832-tuner_fc2580.cc
	rtl2832-tuner_e4k.cc
	baz_udp_source.cc
	baz_udp_sink.cc
)
target_link_libraries(gnuradio-baz ${Boost_LIBRARIES} ${GRUEL_LIBRARIES} ${GNURADIO_CORE_LIBRARIES})
set_target_properties(gnuradio-baz PROPERTIES DEFINE_SYMBOL "gnuradio_baz_EXPORTS")

########################################################################
# Install built library files
########################################################################
install(TARGETS gnuradio-baz
    LIBRARY DESTINATION lib${LIB_SUFFIX} # .so/.dylib file
    ARCHIVE DESTINATION lib${LIB_SUFFIX} # .lib file
    RUNTIME DESTINATION bin              # .dll file
)

########################################################################
# Build and register unit test
########################################################################
#find_package(Boost COMPONENTS unit_test_framework)

#include(GrTest)
#set(GR_TEST_TARGET_DEPS gnuradio-howto)
#turn each test cpp file into an executable with an int main() function
#add_definitions(-DBOOST_TEST_DYN_LINK -DBOOST_TEST_MAIN)

#add_executable(qa_howto_square_ff qa_howto_square_ff.cc)
#target_link_libraries(qa_howto_square_ff gnuradio-howto ${Boost_LIBRARIES})
#GR_ADD_TEST(qa_howto_square_ff qa_howto_square_ff)

#add_executable(qa_howto_square2_ff qa_howto_square2_ff.cc)
#target_link_libraries(qa_howto_square2_ff gnuradio-howto ${Boost_LIBRARIES})
#GR_ADD_TEST(qa_howto_square2_ff qa_howto_square2_ff)
