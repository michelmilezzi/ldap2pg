default:

rpm:
	make -C ../../packaging rpm

tests:
	touch bash_history
	docker-compose up --abort-on-container-exit runner

clean:
	make -C ../../packaging clean
	docker-compose down -v

debug:
	docker-compose exec runner /usr/bin/env $(shell sed 's/^/LDAP/;s/ \+/=/g' ../../ldaprc) /bin/bash

pytest:
	find ../.. -name "*.pyc" -delete
# Looks like ./ldaprc is ignored in CentOS7 by libldap and tools. Put it in envs.
	cd ../.. && env $(shell sed 's/^/LDAP/;s/ \+/=/g' ../../ldaprc) pytest tests/func/ $(filter-out $@,$(MAKECMDGOALS))

%:
	@echo Passing $@ as argument.
