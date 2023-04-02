CC = gcc
CFLAGS = -std=c11 -Wall -Werror -Wextra -g
GCOV_FLAG = -fprofile-arcs -ftest-coverage -fPIC -O0
GCOV_FLAG_TEST = --coverage
TEST_FLAG = -lcheck
LINUX_FLAG = -lm -lsubunit -lrt -lpthread
ifeq ($(shell uname), Linux)
	TEST_FLAG += $(LINUX_FLAG)
endif
SOURCES_1 = _sscanf.c
SOURCES_2 = _sscanf.o
SOURCES_3 = test/test.c
SOURCES_4 = test.o

all: clean string.a

string.a:
	$(CC) $(CFLAGS) -c $(SOURCES_1)
	ar rc _string.a $(SOURCES_2)
	ranlib _string.a
	-rm -rf *.o

test_string.a:
	$(CC) $(CFLAGS) $(GCOV_FLAG) -c $(SOURCES_1)
	ar rc _string.a $(SOURCES_2)
	ranlib _string.a

test_build: clean test_string.a
	$(CC) $(CFLAGS) -c $(SOURCES_3)
	$(CC) $(CFLAGS) $(GCOV_FLAG_TEST) -o tests $(SOURCES_4) _string.a $(TEST_FLAG)

test: test_build
	-rm -rf *.o
	./tests

gcov_report: clean test
	gcovr -r . --html-details -o report_string.html

clean:
	-rm -rf *.o *.a *.out *.gcda *.gch *.gcno *.html *.css *.log log.txt *.png *.info
	-rm -f tests

style:
	clang-format -n *.c *.h

