# Lab Report 3
## Command options of `grep`
### Introduction of `grep`
`grep` can search specific patterns in one or more files. It stands for ***global regular expression print***. `grep` can be used in this way: `grep PATTERN PathOfFile`.
### Other options of `grep`
`grep` can only be used for files, but cannot be used on directories. If we directly use it on a directory, the output would report error. 
```
skill-demo1-data % grep "Lucayans" written_2 
grep: written_2: Is a directory
```
---
However, sometimes we want to search a word within the whole file. In this situation, we can use `grep -r`. The `r` stands for recursive, which means that this command will search through all directories and subdirectories.
For instance, if we want to search for *Lucayans* in the file *written_2*, we can type `grep -r "Lucayans" .`. The output is
```
./travel_guides/berlitz2/Bahamas-History.txt:Centuries before the arrival of Columbus, a peaceful Amerindian people who called themselves the Luccucairi had settled in the Bahamas. Originally from South America, they had traveled up through the Caribbean islands, surviving by cultivating modest crops and from what they caught from sea and shore. Nothing in the experience of these gentle people could have prepared them for the arrival of the Pinta, the Niña, and the Santa Maria at San Salvador on 12 October 1492. Columbus believed that he had reached the East Indies and mistakenly called these people Indians. We know them today as the Lucayans. Columbus claimed the island and others in the Bahamas for his royal Spanish patrons, but not finding the gold and other riches he was seeking, he stayed for only two weeks before sailing towards Cuba.
./travel_guides/berlitz2/Bahamas-History.txt:The Spaniards never bothered to settle in the Bahamas, but the number of shipwrecks attest that their galleons frequently passed through the archipelago en route to and from the Caribbean, Florida, Bermuda, and their home ports. On Eleuthera the explorers dug a fresh-water well — at a spot now known as “Spanish Wells” — which was used to replenish the supplies of water on their ships before they began the long journey back to Europe with their cargoes of South American gold. As for the Lucayans, within 25 years all of them, perhaps some 30,000 people, were removed from the Bahamas to work — and die — in Spanish gold mines and on farms and pearl fisheries on Hispaniola (Haiti), Cuba, and elsewhere in the Caribbean.
```
This command is very useful in searching for a pattern in a large number of files, or when you are unsure which file contains the information you are looking for. If I am not sure would any of the files is talking about pneumonia, I could type `grep -r "pneumonia" .`, and the out put is
```
./travel_guides/berlitz2/Portugal-WhereToGo.txt:On 13 May 1917, three young shepherds claimed they saw a series of miraculous visions of the Virgin Mary — said to disclose three secrets, or prophecies, to the children — followed by a solar phenomenon witnessed by thousands in October of the same year. (Two of the children died of pneumonia soon after these inexplicable events; the third, Lucia, now in her 90s, has been a cloistered Carmelite nun in Coimbra since 1929 and makes very few public appearances.)
```
> Information acquired from [ChatGPT](https://chat.openai.com/chat).
---
Sometimes we may only want to check about how many times a word was mentioned. For instance, if you are a reviewer of films and you want to check the cursing words within the script, you would care about where they are. `grep -n` would solve the problem by showing the number of the line.
`grep -n` would only show how many times a specific pattern is shown. In below example, I would use a file storing the result of `find . -name "*.txt"`. I want to know how many files are named with "Beijing", so I used `grep -n "Beijing" find-results.txt`. The out put is:
```
201:./travel_guides/berlitz2/Beijing-History.txt
212:./travel_guides/berlitz2/Beijing-WhereToGo.txt
224:./travel_guides/berlitz2/Beijing-WhatToDo.txt
```
I could go to the file *Beijing-History.txt* and further check about where Chinese dynasty "Ming" was mentioned. `grep -n "Beijing" ./travel-guides/berlitz2/Beijing-History.txt`. The output is:
```
14:The Ming Period
15:The Mongol rulers of the Yuan Dynasty were eventually undone by indigenous Chinese rebels who established one of the most renowned of all imperial lines, the Ming Dynasty (1368–1644). The capital was again razed and rebuilt, and Ming Emperor Yongle gave it a new name that would stick: Beijing (Northern Capital). By 1420 he had finished constructing the city’s most famous surviving monument, the Forbidden City. This was accompanied by other monumental projects. The Bell Tower, the Drum Tower, and above all, the graceful Temple of Heaven were built in the early 15th century. Many of Beijing’s major temples also date from the Ming Dynasty.
16:The Ming rulers cautiously welcomed a few Catholic missionaries from Europe to Beijing. In the 17th century the Jesuits, headed by Matteo Ricci, had a profound influence not so much on Chinese religion (they made few converts among Beijingers) as on science, mathematics, astronomy, art, medicine, and other forms of knowledge that had never before been infused with Western ideas in China. Perhaps the greatest project of the Ming, however, was the restoration and extension of the Great Wall north of Beijing. For the first time, brick was used to finish these magnificent fortifications. It is the Ming Dynasty Great Wall that millions visit today at Beijing.
18:The Ming rulers were understandably nervous about yet another invasion from the north and took defensive measures by extending the Great Wall. They were nonetheless undone by precisely what they feared most: northern invaders. This time the conquerors were the Manchus, who established a dynasty that proved as long-lived and as glorious as the Ming.
20:Two of the greatest Qing emperors, Kangxi and his grandson Qianlong, maintained the Ming Tombs and saw to the building of the Summer Palace, while the last great imperial ruler of China, the Empress Dowager Cixi, kept the Summer Palace and the Forbidden City in splendid condition into the early 20th century. These and most other historic sites at Beijing were either preserved or created by the Qing rulers, including their own imperial tombs, which rival those of the Ming.
21:The Qing Dynasty is also celebrated for its elaboration of the artistic traditions it inherited from the Ming Dynasty. What we know as Peking-style opera and still see performed today in the capital became formalized under the Qing, although its roots (and costumes) go back to Ming and earlier eras. The Ming were also noted for their superb ink paintings, cloisonné enamel work, furniture design, and lacquerware — but above all for their porcelains of the “five-colors” and “blue-and-white” schools. At the end of the Ming, these porcelains with landscape and garden designs became all the rage in Europe, where imitation “Chinese” pottery began to be produced. The Qing continued these artistic traditions, adding increasingly rich and dense ornamentation and applying new colors, many of them clashing or gaudy.
34:The skyline of the capital rises higher and higher each year, glass and steel replace brick and mud in the old courtyards, cars replace carts in the streets, and computers replace abacuses in the schools. Today’s Beijing would seem to have little in common with the Beihai lakeshore of Kublai Khan and Marco Polo, the Forbidden City of the Ming, the Summer Palace of the Qing, the Temple of Confucius, or even the patriotic tomb of Chairman Mao. But China’s capital has not escaped the history that shaped it, be it ancient or modern. Visitors can still see both today.
```
> Information acquired from [ChatGPT](https://chat.openai.com/chat).
---
If I am aassesor of the film instead of reviewer, I would only care about how many times cursing word has shown. In this case, `grep -c` would help by only showing the number of times the pattern was found.
If I want to check how many times "China" was mentioned in the file *written_2*, I could use `grep -c "Shanghai" find-results.txt`. The output is:
```
3
```
If I want to see how many times was Mongol dynasty "Yuan" was mentioned in *Beijing-History.txt*, I can do `grep -c "Yuan" ./travel_guide/berlitz2/Beijing-History.txt`, and the output is:
```
2
```
> Information acquired from [ChatGPT](https://chat.openai.com/chat).
---
If I am lazier and only want to check about the existence of a word, I can use `grep -q`, which is the quiet mode of grep. A zero exit status would be returned if matches were found.
For instance, I want to see if *Italy* was mentioned in the file names, I can use `grep -q "Italy" find-results.txt` and then see the exit status `echo $?`, the output should be
```
hix@Xiaohes-MacBook-Air written_2 % grep -q "Italy" find-results.txt 
hix@Xiaohes-MacBook-Air written_2 % echo $?
0
```
If I am searching something that does not exist, like "Henry Li", the output would be:
```
hix@Xiaohes-MacBook-Air written_2 % grep -q "Henry Li" find-results.txt 
hix@Xiaohes-MacBook-Air written_2 % echo $?
1
```
> Information acquired from [ChatGPT](https://chat.openai.com/chat).
