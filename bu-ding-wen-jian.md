```
--- Python-2.7.13_orig/Makefile.pre.in	2016-12-18 04:05:06.000000000 +0800
+++ Python-2.7.13/Makefile.pre.in	2017-03-20 11:02:10.567394114 +0800
@@ -245,6 +245,7 @@
 ##########################################################################
 # Parser
 PGEN=		Parser/pgen$(EXE)
+HOSTPGEN=	$(PGEN)$(EXE)
 
 PSRCS=		\
 		Parser/acceler.c \
@@ -681,7 +682,7 @@
 
 $(GRAMMAR_H): @GENERATED_COMMENT@ $(GRAMMAR_INPUT) $(PGEN)
 	@$(MKDIR_P) Include
-	$(PGEN) $(GRAMMAR_INPUT) $(GRAMMAR_H) $(GRAMMAR_C)
+	$(HOSTPGEN) $(GRAMMAR_INPUT) $(GRAMMAR_H) $(GRAMMAR_C)
 $(GRAMMAR_C): @GENERATED_COMMENT@ $(GRAMMAR_H)
 	touch $(GRAMMAR_C)
 
@@ -1121,27 +1122,27 @@
 			$(DESTDIR)$(LIBDEST)/distutils/tests ; \
 	fi
 	PYTHONPATH=$(DESTDIR)$(LIBDEST)  $(RUNSHARED) \
-		$(PYTHON_FOR_BUILD) -Wi -tt $(DESTDIR)$(LIBDEST)/compileall.py \
+		$(HOSTPYTHON) -Wi -tt $(DESTDIR)$(LIBDEST)/compileall.py \
 		-d $(LIBDEST) -f \
 		-x 'bad_coding|badsyntax|site-packages|lib2to3/tests/data' \
 		$(DESTDIR)$(LIBDEST)
 	PYTHONPATH=$(DESTDIR)$(LIBDEST) $(RUNSHARED) \
-		$(PYTHON_FOR_BUILD) -Wi -tt -O $(DESTDIR)$(LIBDEST)/compileall.py \
+		$(HOSTPYTHON) -Wi -tt $(DESTDIR)$(LIBDEST)/compileall.py \
 		-d $(LIBDEST) -f \
 		-x 'bad_coding|badsyntax|site-packages|lib2to3/tests/data' \
 		$(DESTDIR)$(LIBDEST)
 	-PYTHONPATH=$(DESTDIR)$(LIBDEST)  $(RUNSHARED) \
-		$(PYTHON_FOR_BUILD) -Wi -t $(DESTDIR)$(LIBDEST)/compileall.py \
+		$(HOSTPYTHON) -Wi -tt $(DESTDIR)$(LIBDEST)/compileall.py \
 		-d $(LIBDEST)/site-packages -f \
 		-x badsyntax $(DESTDIR)$(LIBDEST)/site-packages
 	-PYTHONPATH=$(DESTDIR)$(LIBDEST) $(RUNSHARED) \
-		$(PYTHON_FOR_BUILD) -Wi -t -O $(DESTDIR)$(LIBDEST)/compileall.py \
+		$(HOSTPYTHON) -Wi -tt $(DESTDIR)$(LIBDEST)/compileall.py \
 		-d $(LIBDEST)/site-packages -f \
 		-x badsyntax $(DESTDIR)$(LIBDEST)/site-packages
 	-PYTHONPATH=$(DESTDIR)$(LIBDEST) $(RUNSHARED) \
-		$(PYTHON_FOR_BUILD) -m lib2to3.pgen2.driver $(DESTDIR)$(LIBDEST)/lib2to3/Grammar.txt
+		$(HOSTPYTHON) -m lib2to3.pgen2.driver $(DESTDIR)$(LIBDEST)/lib2to3/Grammar.txt
 	-PYTHONPATH=$(DESTDIR)$(LIBDEST) $(RUNSHARED) \
-		$(PYTHON_FOR_BUILD) -m lib2to3.pgen2.driver $(DESTDIR)$(LIBDEST)/lib2to3/PatternGrammar.txt
+		$(HOSTPYTHON) -m lib2to3.pgen2.driver $(DESTDIR)$(LIBDEST)/lib2to3/PatternGrammar.txt
 
 # Create the PLATDIR source directory, if one wasn't distributed..
 $(srcdir)/Lib/$(PLATDIR):

```



