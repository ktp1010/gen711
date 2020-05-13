To start, I downloaded all of the software I would need to complete this lab. I downloaded conda, sudo, iqtree and mafft using the following code.
> Mkdir final711  
> Mkdir ananconda  
> cd anaconda  
> curl -LO https://repo.anaconda.com/archive/Anaconda3-5.1.0-Linux-x86_64.sh   
> bash Anaconda3-5.1.0-Linux-x86_64.sh -b -p $HOME/anaconda/install/  
> echo ". $HOME/anaconda/install/etc/profile.d/conda.sh" >> ~/.bashrc  
> source ~/.bashrc  
> conda update -n base conda   
> conda create -y --name gen711  
> sudo apt-get update  
> sudo apt-get -y upgrade  
> sudo apt install iqtree  
> sudo apt install mafft  
> Cd final711  

Once that was done, I dowloaded the data I used from the ensemble database. I chose to use the peptide sequences for two main reasons. The first reason was it fit my biological question, but the primary reason was storage space and the time it took to download, particularly for the human genome. 
> wget ftp://ftp.ensembl.org/pub/release-100/fasta/mus_musculus/pep/Mus_musculus.GRCm38.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-99/fasta/octodon_degus/pep/Octodon_degus.OctDeg1.0.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-99/fasta/castor_canadensis/pep/Castor_canadensis.C.can_genome_v1.0.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-99/fasta/urocitellus_parryii/pep/Urocitellus_parryii.ASM342692v1.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-99/fasta/cavia_porcellus/pep/Cavia_porcellus.Cavpor3.0.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-99/fasta/rattus_norvegicus/pep/Rattus_norvegicus.Rnor_6.0.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-99/fasta/peromyscus_maniculatus_bairdii/pep/Peromyscus_maniculatus_bairdii.HU_Pman_2.1.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-99/fasta/ictidomys_tridecemlineatus/pep/Ictidomys_tridecemlineatus.SpeTri2.0.pep.all.fa.gz  
> wget ftp://ftp.ensembl.org/pub/release-100/fasta/homo_sapiens/pep/Homo_sapiens.GRCh38.pep.all.fa.gz  
 
 Next, I unzipped the files using the gzip - d command
> gzip -d Mus_musculus.GRCm38.pep.all.fa.gz  
> gzip -d Octodon_degus.OctDeg1.0.pep.all.fa.gz  
> gzip -d Castor_canadensis.C.can_genome_v1.0.pep.all.fa.gz  
> gzip -d Urocitellus_parryii.ASM342692v1.pep.all.fa.gz  
> gzip -d Cavia_porcellus.Cavpor3.0.pep.all.fa.gz  
> gzip -d Rattus_norvegicus.Rnor_6.0.pep.all.fa.gz  
> gzip -d Peromyscus_maniculatus_bairdii.HU_Pman_2.1.pep.all.fa.gz  
> gzip -d Ictidomys_tridecemlineatus.SpeTri2.0.pep.all.fa.gz  
> gzip -d Homo_sapiens.GRCh38.pep.all.fa.gz  
 
 The files were unfortunately wrapped, thus I used the following commands to change their formatting into a more accessible form for the purpose of my lab.
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Mus_musculus.GRCm38.pep.all.fa > mouse_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Octodon_degus.OctDeg1.0.pep.all.fa > degu_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Castor_canadensis.C.can_genome_v1.0.pep.all.fa >beaver_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Urocitellus_parryii.ASM342692v1.pep.all.fa > groundsquirrel_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Cavia_porcellus.Cavpor3.0.pep.all.fa > guineapig_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Rattus_norvegicus.Rnor_6.0.pep.all.fa > rat_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Peromyscus_maniculatus_bairdii.HU_Pman_2.1.pep.all.fa > deermouse_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Ictidomys_tridecemlineatus.SpeTri2.0.pep.all.fa > squirrel_unwrap.fa  
> awk '{if(NR==1) {print $0} else {if($0 ~ /^>/) {print "\n"$0} else {printf $0}}}' Homo_sapiens.GRCh38.pep.all.fa > human_unwrap.fa  
 
I wanted to know the evolutionary relationship of the Insr gene in rodents and its relationship to humans. To do this, I messed around with grep commands to find the particular insulin related gene I needed, as there were many when the term "insulin" was used. I find the insulin receptor gene, there were two grep searches I used; "gene_symbol: Insr" or "gene_symbol: INSR". Both of these terms brought up the same gene, but each file had a different fromatting for the capitalization of this gene.
> grep -A 1 "gene_symbol:Insr " mouse_unwrap.fa > mouse_insr.fa  
> grep -A 1 "gene_symbol:INSR " degu_unwrap.fa > degu_insr.fa  
> grep -A 1 "gene_symbol:Insr " beaver_unwrap.fa > beaver_insr.fa  
> grep -A 1 "gene_symbol:INSR " groundsquirrel_unwrap.fa > groundsquirrel_insr.fa  
> grep -A 1 "gene_symbol:INSR " guineapig_unwrap.fa > guineapig_insr.fa  
> grep -A 1 "gene_symbol:Insr " rat_unwrap.fa > rat_insr.fa  
> grep -A 1 "gene_symbol:Insr " deermouse_unwrap.fa > deermouse_insr.fa  
> grep -A 1 "gene_symbol:INSR " squirrel_unwrap.fa > squirrel_insr.fa  
> grep -A 1 "gene_symbol:INSR " human_unwrap.fa > human_insr.fa  
 
 Next, the headers of these files were long with information unneccessary for the question I was asking. Thus, using the folling commands, I renamed the headers to (species name_) for ease of reading the files and the pulled sequences. It is also useful to have the shorter headers when constructing the phylogenetic tree.
> awk '/^>/{print ">mouse_" ++i; next}{print}' mouse_insr.fa > header_mouse_insr.fa  
> awk '/^>/{print ">degu_" ++i; next}{print}' degu_insr.fa > header_degu_insr.fa  
> awk '/^>/{print ">beaver_" ++i; next}{print}' beaver_insr.fa > header_beaver_insr.fa  
> awk '/^>/{print ">groundsquirrel_" ++i; next}{print}' groundsquirrel_insr.fa > header_groundsquirrel_insr.fa  
> awk '/^>/{print ">guineapig_" ++i; next}{print}' guineapig_insr.fa > header_guineapig_insr.fa  
> awk '/^>/{print ">rat_" ++i; next}{print}' rat_insr.fa > header_rat_insr.fa  
> awk '/^>/{print ">squirrel_" ++i; next}{print}' squirrel_insr.fa > header_squirrel_insr.fa  
> awk '/^>/{print ">human_" ++i; next}{print}' human_insr.fa > header_human_insr.fa  
 
Next, I combined the new files made in the previous step into a single file
> cat header_beaver_insr.fa header_deermouse_insr.fa header_degu_insr.fa header_groundsquirrel_insr.fa header_guineapig_insr.fa header_human_insr.fa header_mouse_insr.fa header_rat_insr.fa header_squirrel_insr.fa > header_complete.fa   

Next, I used mafft with the default multiple sequence alignment settings.
> mafft --auto header_complete.fa > insr_complete.fa  
 
Next, I used iqtree to contruct the phylogenetic tree.
> iqtree -s insr_complete.fa -m LG -bb 1000 -pre insr  

To construct the tree, I used cat on the contree file produced by this command, and copy and pasted the information into FigTree v1.4.4. Once in this program, I rerooted the tree to have humans as the outgroup. I added the bootstrap value labels to the nodes. Finally, I aligned the tip labels, as I found the tree to be easier to read and more aesthetically pleasing that way.

The constructed tree can be seen below


#NEXUS
begin trees;
	tree tree_1 = [&R] ((((((deermouse_1:0.001199,(deermouse_2:2.0E-6,deermouse_3:2.0E-6)[&label=99]:0.007788)[&label=100]:0.037253,mouse_1:0.091804)[&label=58]:0.014074,((mouse_2:2.0E-6,mouse_3:9.34E-4)[&label=93]:0.003322,(rat_1:2.0E-6,rat_2:0.00223)[&label=89]:0.005427)[&label=50]:0.004501)[&label=100]:0.030318,((((degu_1:3.0E-6,degu_4:0.012785)[&label=92]:0.001047,(degu_2:4.38E-4,degu_3:5.82E-4)[&label=100]:0.022919)[&label=100]:0.042368,(guineapig_1:2.0E-6,guineapig_2:2.0E-6)[&label=100]:0.020549)[&label=100]:0.022846,((groundsquirrel_1:7.44E-4,groundsquirrel_2:2.0E-6)[&label=61]:2.0E-6,(squirrel_1:2.0E-6,squirrel_2:3.0E-6)[&label=100]:0.0078)[&label=100]:0.025336)[&label=95]:0.007574)[&label=53]:0.002272,(beaver_1:2.0E-6,(((beaver_2:0.033162,(beaver_5:3.0E-6,beaver_7:0.007499)[&label=100]:0.020726)[&label=100]:0.014355,beaver_3:0.005802)[&label=39]:0.001011,(beaver_4:2.92E-4,beaver_6:0.002284)[&label=65]:0.004955)[&label=96]:0.00751)[&label=100]:0.052369)[&label=87,!color=#000000]:0.007172,((human_1:2.0E-6,human_2:2.0E-6)[&label=72]:0.001652,human_3:0.032316)[&label=87,!color=#000000]:0.007172);
end;

