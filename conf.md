1. Download the Latest Version of Python Source Code
===========================================================
cd /tmp

wget https://www.python.org/ftp/python/3.10.6/Python-3.10.6.tgz

Extract Compressed Files
-------------------------

tar -xf Python-3.10.6.tgz

Install a Second Instance of Python 
------------------------------------
sudo make altinstall

(Option) Overwrite Default Python Installation 
----------------------------------------------
sudo make install

Verify Python Version
---------------------
python3 --version


2. change python default version on ubuntu
=======================================

sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.10.6 1

sudo update-alternatives  --set python /usr/bin/python3.10.6

change python default version on ubuntu (alternative)
======================================================
cd /usr/bin/
rm python3
ln -s python3.10.6 python3


3. Dashboard Test
===================

first run black:
------------------

black --skip-string-normalization --line-length=120 src
black --skip-string-normalization --line-length=120 tests

then run isort
----------------

isort --atomic --profile black src
isort --atomic --profile black tests

then run mypy
----------------

cd src && mypy .

then run static validation
----------------------------

DJANGO_SETTINGS_MODULE=invoizpaid.settings.dev ./scripts/static_validate_backend.sh

DJANGO_SETTINGS_MODULE=invoizpaid.settings.dev ./scripts/test_ci_backend.sh

then finally run test
----------------------
py.test -n 4 --disable-socket --nomigrations --reuse-db -W error::RuntimeWarning --cov=src --cov-report=html tests/python/lifecycle/test_views.py::TestLifeCycleDeleteGuarantorView::test_lifecycle_guarantor_stage_success_delete_guarantor

py.test -n 4 --disable-socket --nomigrations --reuse-db -W error::RuntimeWarning --cov=src --cov-report=html tests/python/lifecycle/test_views.py::TestLifeCycleEligibleTermsView::test_lifecycle_eligible_terms_tier1_tier2

py.test -n 4 --disable-socket --nomigrations --reuse-db -W error::RuntimeWarning --cov=src --cov-report=html tests/python/lib/test_eligibleterms.py::TestUnderwritingManager::test_calculate_eligible_terms

py.test -n 4 --disable-socket --nomigrations --reuse-db -W error::RuntimeWarning --cov=src --cov-report=html tests/python/utils/nigeria/test_underwriting_utils.py::TestUnderwritingManager

py.test -n 4 --disable-socket --nomigrations --reuse-db -W error::RuntimeWarning --cov=src --cov-report=html tests/

py.test -n 8  -W error::RuntimeWarning --reuse-db --cov=src --cov-report=html tests/

4. mypy error: Positional-only parameters are only supported in Python 3.8 and greater
=======================================================================================

upgrade mypy (pip install)

5. static validation error: WARNING: unable to find a config; path `../.semgrep_rules.yml` does not exist
invalid configuration file found (1 configs were invalid)
===========================================================================================================

run ./scripts/get_static_validation_backends.sh

then re-run DJANGO_SETTINGS_MODULE=invoizpaid.settings.dev ./scripts/static_validate_backend.sh


5. python permission error
==================================
original pip = #!/usr/local/bin/python3
original poetry = #!/home/ojapay/dashboard/env/bin/python

6. remove symbolic link (symlink)
====================================
sudo unlink Docs


7. remove python from ubuntu
==============================
sudo apt-get remove python3

8. install python from wget on ubuntu
======================================
sudo apt update

sudo apt install wget build-essential checkinstall

sudo wget https://python.org/ftp/python/3.10.6/Python-3.10.6.tgz

cd Python-3.10.6

ls

sudo ./configure --enable-optimizations

sudo make altinstall ##for another version

or

sudo make install ##to override existing version

python3.10 --version


9. Sub-process /usr/bin/dpkg returned an error code (1)
=========================================================

sudo mv /var/lib/dpkg/info /var/lib/dpkg/info_silent

sudo mkdir /var/lib/dpkg/info

sudo apt-get update

sudo apt-get -f install

sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info_silent

sudo rm -rf /var/lib/dpkg/info

sudo mv /var/lib/dpkg/info_silent /var/lib/dpkg/info

sudo apt-get update

sudo apt-get upgrade

10. cannot find module '_bz2'
==================================

sudo cp /usr/lib/python3.10/lib-dynload/_bz2.cpython-310-x86_64-linux-gnu.so  /usr/local/
lib/python3.10/

11. Rebase branch with master branch
======================================

checkout to master
------------------
git checkout master

pull master
-------------
git pull

checkout to my branch
----------------------
git checkout yourbranch

update (rebase) my branch
---------------------------
git rebase master

if there are conflicts, resolve it in my files where the conflict is
then,

git rebase --continue

push to branch
---------------
git push -f

12. git
=========
https://media.giphy.com/media/8du24IW5k6fimUSeU5/giphy.gif

13. exclude or ignore some files from git commit
=================================================
git update-index --assume-unchanged filepath
git update-index --assume-unchanged default/config.php


14. poetry cannot run some installations
========================================
sudo rm -rf ~/.cache/pypoetry

15. squashing all commits
============================

rebase your branch
-------------------
git rebase -i HEAD~3

# add `s` or `squash` to all the other commits except the one on top which should have `pick`
# in nano or vim editor and save (ctrl x, Y, Enter for nano or ESC :wq! for vim)

if there are conflicts
----------------------
git rebase --continue

git status

# edit conflict in vscode

add the fixed files
--------------------
# git add <fixed_files>

continue rebase
------------------
git rebase --continue 

# In nano editor, chose my commit text
# in nano or vim editor and save (ctrl x, Y, Enter for nano or ESC :wq! for vim)

push to branch
-------------
git push -f


16. shell plus
=================
import logging

logging.getLogger('parso.python.diff').disabled = True
logging.getLogger('parso.cache').disabled = True
logging.getLogger('matplotlib').disabled = True
logging.getLogger('matplotlib.pyplot').disabled = True

In [3]: stage=LoanApplicationLifeCycle.objects.get(id='0cfd751d-bb17-4cc8-9784-1b6cdb665f62')

In [4]: user=User.objects.get(email='kennedy@lendigo.ng')

In [5]: stage.assignee
Out[5]: <User: lendigo@quickcheck.ng>

In [6]: stage.assignee = user

In [7]: stage.save()


17. use postgres psql
======================

sudo -u postgres psql

18. remove rebase
=======================
git rebase --skip

19. cancel all rebase
=====================
git reflog
