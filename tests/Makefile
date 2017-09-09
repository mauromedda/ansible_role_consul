all : syntax run idempotence

.PHONY: all

syntax:
	ansible-playbook -i inventory test.yml --syntax-check

run:
	ansible-playbook -i inventory test.yml --connection=local --sudo

idempotence:
	ansible-playbook -i inventory test.yml --connection=local --sudo | grep -q 'changed=0.*failed=0' \
	&& (echo 'Idempotence test: pass' && exit 0) || (echo 'Idempotence test: fail' && exit 1)

