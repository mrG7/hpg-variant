CC = gcc
CFLAGS = -std=c99 -O3 -march=native -D_XOPEN_SOURCE=600 -D_GNU_SOURCE
CFLAGS_DEBUG = -std=c99 -g -O0 -D_XOPEN_SOURCE=600 -D_GNU_SOURCE

# Source code folders
ROOT_DIR = $(PWD)/../..
INC_DIR = $(ROOT_DIR)/include
LIBS_DIR = $(ROOT_DIR)/libs
SRC_DIR = $(ROOT_DIR)/src
BIN_DIR = $(ROOT_DIR)/bin
TEST_DIR = $(ROOT_DIR)/test

# Libraries folders
BIOINFO_LIBS_DIR = $(LIBS_DIR)/bioinfo-libs
COMMON_LIBS_DIR = $(LIBS_DIR)/common-libs
CONTAINERS_DIR = $(COMMON_LIBS_DIR)/containers
COMMONS_DIR = $(COMMON_LIBS_DIR)/commons
BIOFORMATS_DIR = $(BIOINFO_LIBS_DIR)/bioformats
MATH_DIR = $(LIBS_DIR)/math

# -I (includes) and -L (libraries) paths
INCLUDES = -I $(SRC_DIR) -I $(LIBS_DIR) -I $(BIOINFO_LIBS_DIR) -I $(COMMON_LIBS_DIR) -I $(INC_DIR) -I /usr/include/libxml2 -I/usr/local/include
LIBS = -L/usr/lib/x86_64-linux-gnu -lcurl -Wl,-Bsymbolic-functions -lconfig -lcprops -fopenmp -lm -lxml2 -lgsl -lgslcblas -largtable2
LIBS_TEST = -lcheck

INCLUDES_STATIC = -I $(SRC_DIR) -I $(LIBS_DIR) -I $(BIOINFO_LIBS_DIR) -I $(COMMON_LIBS_DIR) -I $(INC_DIR) -I /usr/include/libxml2 -I/usr/local/include
LIBS_STATIC = -L$(LIBS_DIR) -L/usr/lib/x86_64-linux-gnu -lcurl -Wl,-Bsymbolic-functions -lconfig -lcprops -fopenmp -lm -lxml2 -lgsl -lgslcblas -largtable2


# Project dependencies
VCF_OBJS = $(BIOFORMATS_DIR)/vcf/vcf_*.o
GFF_OBJS = $(BIOFORMATS_DIR)/gff/gff_*.o
PED_OBJS = $(BIOFORMATS_DIR)/ped/ped_*.o
REGION_TABLE_OBJS = $(BIOFORMATS_DIR)/features/region/region.o $(BIOFORMATS_DIR)/features/region/region_table.o $(BIOFORMATS_DIR)/features/region/region_table_utils.o
MISC_OBJS = $(COMMONS_DIR)/file_utils.o $(COMMONS_DIR)/string_utils.o $(COMMONS_DIR)/http_utils.o $(COMMONS_DIR)/log.o $(COMMONS_DIR)/result.o \
	$(CONTAINERS_DIR)/array_list.o $(CONTAINERS_DIR)/list.o $(BIOFORMATS_DIR)/family.o $(MATH_DIR)/fisher.o
DEPEND_OBJS = $(VCF_OBJS) $(GFF_OBJS) $(PED_OBJS) $(REGION_TABLE_OBJS) $(MISC_OBJS)

# Project files
VCF_TOOLS_FILES = $(SRC_DIR)/vcf-tools/*.c $(SRC_DIR)/vcf-tools/filter/*.c $(SRC_DIR)/vcf-tools/merge/*.c $(SRC_DIR)/vcf-tools/split/*.c $(SRC_DIR)/vcf-tools/stats/*.c $(GLOBAL_FILES) $(SRC_DIR)/shared_options.c $(SRC_DIR)/hpg_variant_utils.c
VCF_TOOLS_OBJS = $(SRC_DIR)/vcf-tools/*.o $(SRC_DIR)/vcf-tools/filter/*.o $(SRC_DIR)/vcf-tools/merge/*.o $(SRC_DIR)/vcf-tools/split/*.o $(SRC_DIR)/vcf-tools/stats/*.o $(SRC_DIR)/*.o


# hpg-var-vcf targets
vcf-dist: vcf-obj-dist
	$(CC) $(CFLAGS) -o $(BIN_DIR)/hpg-var-vcf $(VCF_TOOLS_OBJS) $(DEPEND_OBJS) $(INCLUDES_STATIC) $(LIBS)

vcf-obj-dist: $(VCF_TOOLS_FILES)
	for F in $(VCF_TOOLS_FILES); do \
		$(CC) $(CFLAGS) -c $$F -o $$F.o $(INCLUDES_STATIC) $(LIBS); \
	done;

vcf-debug: vcf-obj-debug
	$(CC) $(CFLAGS_DEBUG) -o $(BIN_DIR)/hpg-var-vcf $(VCF_TOOLS_OBJS) $(DEPEND_OBJS) $(INCLUDES) $(LIBS)

vcf-obj-debug: $(VCF_TOOLS_FILES)
	for F in $(VCF_TOOLS_FILES); do \
		$(CC) $(CFLAGS_DEBUG) -c $$F -o $$F.o $(INCLUDES) $(LIBS); \
	done;
