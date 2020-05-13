> Mkdir final711
> Mkdir ananconda
> cd anaconda
curl -LO https://repo.anaconda.com/archive/Anaconda3-5.1.0-Linux-x86_64.sh
bash Anaconda3-5.1.0-Linux-x86_64.sh -b -p $HOME/anaconda/install/
echo ". $HOME/anaconda/install/etc/profile.d/conda.sh" >> ~/.bashrc
source ~/.bashrc
conda update -n base conda
conda create -y --name gen711
Cd final711
sudo apt-get update
sudo apt-get -y upgrade
sudo apt install iqtree
sudo apt install mafft



wget ftp://ftp.ensembl.org/pub/release-100/fasta/mus_musculus/pep/Mus_musculus.GRCm38.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/fasta/octodon_degus/pep/Octodon_degus.OctDeg1.0.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/fasta/castor_canadensis/pep/Castor_canadensis.C.can_genome_v1.0.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/fasta/urocitellus_parryii/pep/Urocitellus_parryii.ASM342692v1.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/fasta/cavia_porcellus/pep/Cavia_porcellus.Cavpor3.0.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/fasta/rattus_norvegicus/pep/Rattus_norvegicus.Rnor_6.0.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/fasta/peromyscus_maniculatus_bairdii/pep/Peromyscus_maniculatus_bairdii.HU_Pman_2.1.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-99/fasta/ictidomys_tridecemlineatus/pep/Ictidomys_tridecemlineatus.SpeTri2.0.pep.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-100/fasta/homo_sapiens/pep/Homo_sapiens.GRCh38.pep.all.fa.gz
 
 
gzip -d Mus_musculus.GRCm38.pep.all.fa.gz
gzip -d Octodon_degus.OctDeg1.0.pep.all.fa.gz
gzip -d Castor_canadensis.C.can_genome_v1.0.pep.all.fa.gz
gzip -d Urocitellus_parryii.ASM342692v1.pep.all.fa.gz
gzip -d Cavia_porcellus.Cavpor3.0.pep.all.fa.gz
gzip -d Rattus_norvegicus.Rnor_6.0.pep.all.fa.gz
gzip -d Peromyscus_maniculatus_bairdii.HU_Pman_2.1.pep.all.fa.gz
gzip -d Ictidomys_tridecemlineatus.SpeTri2.0.pep.all.fa.gz
gzip -d Homo_sapiens.GRCh38.pep.all.fa.gz
 
 
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Mus_musculus.GRCm38.pep.all.fa > mouse_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Octodon_degus.OctDeg1.0.pep.all.fa > degu_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Castor_canadensis.C.can_genome_v1.0.pep.all.fa >beaver_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Urocitellus_parryii.ASM342692v1.pep.all.fa > groundsquirrel_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Cavia_porcellus.Cavpor3.0.pep.all.fa > guineapig_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Rattus_norvegicus.Rnor_6.0.pep.all.fa > rat_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Peromyscus_maniculatus_bairdii.HU_Pman_2.1.pep.all.fa > deermouse_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Ictidomys_tridecemlineatus.SpeTri2.0.pep.all.fa > squirrel_unwrap.fa
awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Homo_sapiens.GRCh38.pep.all.fa > human_unwrap.fa
 
 
grep -A 1 "gene_symbol:Insr " mouse_unwrap.fa > mouse_insr.fa
grep -A 1 "gene_symbol:INSR " degu_unwrap.fa > degu_insr.fa
grep -A 1 "gene_symbol:Insr " beaver_unwrap.fa > beaver_insr.fa
grep -A 1 "gene_symbol:INSR " groundsquirrel_unwrap.fa > groundsquirrel_insr.fa
grep -A 1 "gene_symbol:INSR " guineapig_unwrap.fa > guineapig_insr.fa
grep -A 1 "gene_symbol:Insr " rat_unwrap.fa > rat_insr.fa
grep -A 1 "gene_symbol:Insr " deermouse_unwrap.fa > deermouse_insr.fa
grep -A 1 "gene_symbol:INSR " squirrel_unwrap.fa > squirrel_insr.fa
grep -A 1 "gene_symbol:INSR " human_unwrap.fa > human_insr.fa
 
 
awk '/^>/{print ">mouse_" ++i; next}{print}' mouse_insr.fa > header_mouse_insr.fa
awk '/^>/{print ">degu_" ++i; next}{print}' degu_insr.fa > header_degu_insr.fa
awk '/^>/{print ">beaver_" ++i; next}{print}' beaver_insr.fa > header_beaver_insr.fa
awk '/^>/{print ">groundsquirrel_" ++i; next}{print}' groundsquirrel_insr.fa > header_groundsquirrel_insr.fa
awk '/^>/{print ">guineapig_" ++i; next}{print}' guineapig_insr.fa > header_guineapig_insr.fa
awk '/^>/{print ">rat_" ++i; next}{print}' rat_insr.fa > header_rat_insr.fa
awk '/^>/{print ">squirrel_" ++i; next}{print}' squirrel_insr.fa > header_squirrel_insr.fa
awk '/^>/{print ">human_" ++i; next}{print}' human_insr.fa > header_human_insr.fa
 
cat header_beaver_insr.fa header_deermouse_insr.fa header_degu_insr.fa header_groundsquirrel_insr.fa header_guineapig_insr.fa header_human_insr.fa header_mouse_insr.fa header_rat_insr.fa header_squirrel_insr.fa > header_complete.fa
 
mafft --auto header_complete.fa > insr_complete.fa
 
iqtree -s insr_complete.fa -m LG -bb 1000 -pre insr


