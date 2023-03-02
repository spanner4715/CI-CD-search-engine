cd /home/ubuntu/sbert-search-bar
echo "------------BEGIN-------------">/home/ubuntu/logs/sbert-search-bar.txt
echo "last job start: $(date)">>/home/ubuntu/logs/sbert-search-bar.txt
export PATH="/home/ubuntu/miniconda3/bin:${PATH}"
source activate sbar-env
git checkout prod
git stash
git pull origin prod --rebase
pip3 install -r requirements.txt
python3 engine.py>>/home/ubuntu/logs/sbert-search-bar.txt
kill -9 $(pgrep streamlit) || echo "Process Not Found!"
nohup streamlit run app.py &>/dev/null &
echo "last job end: $(date)">>/home/ubuntu/logs/sbert-search-bar.txt

echo "[info] pushing new dataset back to github">>/home/ubuntu/logs/sbert-search-bar.txt
git add data/project_mappings.csv
git commit -m "[searchbar-server autocommit] training data updated @ timestamp $(date +%s)"
git pull origin prod --rebase
git push origin prod
echo "------------END-------------">>/home/ubuntu/logs/sbert-search-bar.txt
