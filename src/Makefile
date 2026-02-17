.PHONY: install run debug clean lint


install: ## dependencies
	pip install . || pip install -r requirements.txt

run: ## run
	python3 a_maze_ing.py config.txt

debug: ## Debug
	python3 -m pdb a_maze_ing.py config.txt

clean: ## Clean up
	find . -type d -name "__pycache__" -exec rm -r {} + 
	find . -type f -name "*.pyc" -delete 
	rm -rf build dist *.egg-info

lint: ## Run linter
	flake8 --max-line-length=88 .
	mypy --warn-return-any .

dev-tools: ## development tools
	pip install flake8 mypy build
