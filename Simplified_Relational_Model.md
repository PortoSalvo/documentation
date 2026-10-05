# Simplified Relational Model

This model is the result of optimizing the Direct Relational Model derived from EA. The optimizations applied include surrogate identifiers, composite key simplification, validation period attributes (dropping `Validation_Period`) and Domain vocabulary representation.

**\#\# Table ENUMS**  
&nbsp;  
Domain(<u>domain\_id</u>, domain\_name)  
&emsp;&emsp;NOT NULL(domain\_name)  
&emsp;&emsp;UNIQUE(domain\_name)  
&emsp;&emsp;IC-3  
&nbsp;  
Object(<u>object\_id</u>, object\_name, domain\_id)  
&emsp;&emsp;NOT NULL(object\_name)  
&emsp;&emsp;NOT NULL(domain\_id)  
&emsp;&emsp;UNIQUE(object\_name)  
&emsp;&emsp;IC-4  
&nbsp;  
Gender(<u>gender\_id</u>, gender\_name)  
&emsp;&emsp;NOT NULL(gender\_name)  
&emsp;&emsp;UNIQUE(gender\_name)  
&emsp;&emsp;IC-7  
&nbsp;  
Feeding\_Dependency(<u>feeding\_dep\_id</u>, feeding\_dep\_name)  
&emsp;&emsp;NOT NULL(feeding\_dep\_name)  
&emsp;&emsp;UNIQUE(feeding\_dep\_name)  
&emsp;&emsp;IC-11  
&nbsp;  
Meal\_Type(<u>meal\_type\_id</u>, meal\_type\_name)  
&emsp;&emsp;NOT NULL(meal\_type\_name)  
&emsp;&emsp;UNIQUE(meal\_type\_name)  
&emsp;&emsp;IC-9  
&nbsp;  
Meal\_Subtype(<u>meal\_subtype\_id</u>, meal\_subtype\_name)  
&emsp;&emsp;NOT NULL(meal\_subtype\_name)  
&emsp;&emsp;UNIQUE(meal\_subtype\_name)  
&emsp;&emsp;IC-10  
&nbsp;  
Dose\_Measure(<u>dose\_measure\_id</u>, dose\_measure\_name)  
&emsp;&emsp;NOT NULL(dose\_measure\_name)  
&emsp;&emsp;UNIQUE(dose\_measure\_name)  
&emsp;&emsp;IC-47  
&nbsp;  
Administration\_Route(<u>admin\_route\_id</u>, admin\_route\_name)  
&emsp;&emsp;NOT NULL(admin\_route\_name)  
&emsp;&emsp;UNIQUE(admin\_route\_name)  
&emsp;&emsp;IC-19  
&nbsp;  
Occurrence\_Category(<u>occ\_category\_id</u>, occ\_category\_name)  
&emsp;&emsp;NOT NULL(occ\_category\_name)  
&emsp;&emsp;UNIQUE(occ\_category\_name)  
&emsp;&emsp;IC-20, IC-148  
&nbsp;  
Care\_Service\_Category(<u>care\_service\_cat\_id</u>, care\_service\_cat\_name)  
&emsp;&emsp;NOT NULL(care\_service\_cat\_name)  
&emsp;&emsp;UNIQUE(care\_service\_cat\_name)  
&emsp;&emsp;IC-23  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Users, Roles and Permissions**  
&nbsp;  
Role(<u>role\_id</u>, role\_name, description)  
&emsp;&emsp;NOT NULL(role\_name)  
&emsp;&emsp;UNIQUE(role\_name)  
&emsp;&emsp;IC-5  
&nbsp;  
Role\_Domains(<u>role\_id, domain\_id</u>, is\_admin)  
&emsp;&emsp;role\_id: FK(Role)  
&emsp;&emsp;domain\_id: FK(Domain)  
&emsp;&emsp;NOT NULL(is\_admin)  
&emsp;&emsp;IC-5  
&nbsp;  
role\_permissions(<u>role\_id, operation\_name, object\_name</u>)  
&emsp;&emsp;role\_id: FK(Role)  
&emsp;&emsp;operation\_name: ENUM  
&emsp;&emsp;IC-2, IC-6  
&nbsp;  
User(<u>userId</u>, username, password, is\_active, email)  
&emsp;&emsp;NOT NULL(username)  
&emsp;&emsp;NOT NULL(password)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;UNIQUE(username)  
&emsp;&emsp;UNIQUE(email)  
&emsp;&emsp;IC-73, IC-74, IC-182  
user\_roles(<u>userId, role\_id</u>)  
&emsp;&emsp;userId: FK(User)  
&emsp;&emsp;role\_id: FK(Role)  
&emsp;&emsp;IC-132  
&nbsp;  
&nbsp;  
**\#\# Person Hierarchy (and close relations)**  
&nbsp;  
Person(<u>id</u>, cc, name, gender\_id, birth\_date, email, address\_line\_1, address\_line\_2, city, country, zipcode, profile\_image\_path)  
&emsp;&emsp;gender\_id: FK(Gender)  
&emsp;&emsp;NOT NULL(cc)  
&emsp;&emsp;NOT NULL(name)  
&emsp;&emsp;NOT NULL(gender\_id)  
&emsp;&emsp;NOT NULL(birth\_date)  
&emsp;&emsp;NOT NULL(address\_line\_1)  
&emsp;&emsp;NOT NULL(city)  
&emsp;&emsp;NOT NULL(country)  
&emsp;&emsp;NOT NULL(zipcode)  
&emsp;&emsp;UNIQUE(cc)  
&emsp;&emsp;IC-50, IC-74, IC-75, IC-133, IC-162  
&nbsp;  
person\_phone\_number(<u>id, phone\_number</u>)  
&emsp;&emsp;id: FK(Person)  
&emsp;&emsp;IC-51, IC-76, IC-77  
&nbsp;  
Senior\_Reference(<u>id</u>)  
&emsp;&emsp;id: FK(Person)  
&emsp;&emsp;IC-133  
&nbsp;  
Guardian(<u>id</u>, userId)  
&emsp;&emsp;id: FK(Person)  
&emsp;&emsp;userId: FK(User)  
&emsp;&emsp;NOT NULL(userId)  
&emsp;&emsp;IC-73, IC-74, IC-79, IC-133  
&nbsp;  
Collaborator(<u>id</u>, userId, is\_active)  
&emsp;&emsp;id: FK(Person)  
&emsp;&emsp;userId: FK(User)  
&emsp;&emsp;NOT NULL(userId)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-73, IC-74, IC-133, IC-134  
&nbsp;  
Time\_off(<u>time\_off\_id</u>, option\_name)  
&emsp;&emsp;UNIQUE(option\_name)  
&emsp;&emsp;IC-8  
&nbsp;  
Home\_Care\_Collaborator(<u>id</u>, max\_consecutive\_days, weekly\_hours, rating, is\_active,&nbsp;time\_off\_id)  
&emsp;&emsp;id: FK(Collaborator)  
&emsp;&emsp;time\_off\_id: FK(Time\_off)  
&emsp;&emsp;NOT NULL(max\_consecutive\_days)  
&emsp;&emsp;NOT NULL(weekly\_hours)  
&emsp;&emsp;NOT NULL(rating)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-52, IC-53, IC-54, IC-134, IC-152  
&nbsp;  
Day\_Care\_Collaborator(<u>id</u>, is\_active)  
&emsp;&emsp;id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-134, IC-186  
&nbsp;  
time\_off\_days(<u>time\_off\_id</u><u>, day\_of\_week</u>)  
&emsp;&emsp;time\_off\_id: FK(Time\_off)  
&emsp;&emsp;day\_of\_week: ENUM  
&emsp;&emsp;IC-1  
&nbsp;  
Client(<u>id</u>)  
&emsp;&emsp;id: FK(Person)  
&emsp;&emsp;IC-133, IC-135, IC-136, IC-137  
&nbsp;  
Dietary\_Preference(<u>diatery\_pref\_id</u>, dietary\_pref\_description)  
&emsp;&emsp;NOT NULL(dietary\_pref\_description)  
&emsp;&emsp;UNIQUE(dietary\_pref\_description)  
&nbsp;  
client\_dietary\_preference(<u>id, diatery\_pref\_id</u>)  
&emsp;&emsp;id: FK(Client)  
&emsp;&emsp;diatery\_pref\_id: FK(Dietary\_Preference)  
&nbsp;  
Religious\_Belief(<u>religion\_id</u>, religion\_name)  
&emsp;&emsp;NOT NULL(religion\_name)  
&emsp;&emsp;UNIQUE(religion\_name)  
&nbsp;  
client\_religious\_belief(<u>id,</u>&nbsp;<u>religion\_id</u>)  
&emsp;&emsp;id: FK(Client)  
&emsp;&emsp;<u>religion\_id</u>: FK(Religious\_Belief)  
&nbsp;  
&nbsp;  
&nbsp;  
Child(<u>id</u>, student\_number, classroom, photo\_consent, is\_active, age\_group, guardian\_id, relationship)  
&emsp;&emsp;id: FK(Client)  
&emsp;&emsp;age\_group: ENUM  
&emsp;&emsp;guardian\_id: FK(Guardian)  
&emsp;&emsp;UNIQUE(student\_number)  
&emsp;&emsp;NOT NULL(student\_number)  
&emsp;&emsp;NOT NULL(photo\_consent)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;NOT NULL(group\_id)  
&emsp;&emsp;NOT NULL(guardian\_id)  
&emsp;&emsp;IC-31, IC-35, IC-74, IC-135, IC-136, IC-141, IC-156, IC-157, IC-158, IC-159, IC-160, IC-161, IC-167, IC-179, IC-183, IC-184  
&nbsp;  
Patient(<u>id</u>, feeding\_dep\_id, meal\_type\_id, meal\_subtype\_id)  
&emsp;&emsp;id: FK(Client)  
&emsp;&emsp;feeding\_dep\_id: FK(Feeding\_Dependency)  
&emsp;&emsp;meal\_type\_id: FK(Meal\_Type)  
&emsp;&emsp;meal\_subtype\_id: FK(Meal\_Subtype)  
&emsp;&emsp;IC-81, IC-82, IC-135, IC-136, IC-138, IC-139, IC-147, IC-148, IC-157  
&nbsp;  
Home\_Care\_Patient(<u>id</u>, is\_active)  
&emsp;&emsp;id: FK(Patient)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-85, IC-138, IC-139, IC-159  
&nbsp;  
Day\_Care\_Patient(<u>id</u>, is\_active, process\_number, admission\_date)  
&emsp;&emsp;id: FK(Patient)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;NOT NULL(process\_number)  
&emsp;&emsp;NOT NULL(admission\_date)  
&emsp;&emsp;UNIQUE(process\_number)  
&emsp;&emsp;IC-84, IC-138, IC-139, IC-158  
&nbsp;  
senior\_reference\_looks\_after\_patient(<u>senior\_ref\_id, patient\_id</u>, relationship)  
&emsp;&emsp;senior\_ref\_id: FK(Senior\_Reference)  
&emsp;&emsp;patient\_id: FK(Patient)  
&emsp;&emsp;IC-78, IC-140  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Patient Autonomy and Health Condition (Senior Day Care and Home Care Service Specific)**  
&nbsp;  
Autonomy(<u>aut\_name</u>, autonomy\_cat)  
&emsp;&emsp;NOT NULL(autonomy\_cat)  
&emsp;&emsp;autonomy\_cat: ENUM  
&nbsp;  
&nbsp;  
patient\_autonomy\_dependence<u>(patient\_id, aut\_name, valid\_since</u>,&nbsp;<u>autonomy\_dep\_level,</u>valid\_until)  
&emsp;&emsp;patient\_id: FK(Patient)  
&emsp;&emsp;aut\_name: FK(Autonomy)  
&emsp;&emsp;autonomy\_dep\_level: ENUM  
&emsp;&emsp;IC-48, IC-49, IC-72  
&nbsp;  
&emsp;&emsp;Health\_Condition(<u>health\_cond\_id</u>, health\_cat\_name)  
&emsp;&emsp;NOT NULL(health\_cat\_name)  
&emsp;&emsp;health\_cat\_name: ENUM  
&nbsp;  
client\_health\_cond<u>(client\_id, health\_cond\_id, valid\_since,</u>&nbsp;valid\_until, observations)  
&emsp;&emsp;client\_id: FK(Client)  
&emsp;&emsp;health\_cond\_id: FK(Health\_Condition)  
&emsp;&emsp;NOT NULL(client\_id)  
&emsp;&emsp;NOT NULL(health\_cond\_id)  
&emsp;&emsp;NOT NULL(valid\_since)  
&emsp;&emsp;IC-49, IC-72  
&nbsp;  
**\#\# Prescriptions and Medicine\_Administration**  
&nbsp;  
Dose(<u>dose\_id</u>, dose\_measure\_name, quantity)  
&emsp;&emsp;dose\_measure\_name: FK(Dose\_Measure)  
&emsp;&emsp;NOT NULL(dose\_measure\_name)  
&emsp;&emsp;NOT NULL(quantity)  
&emsp;&emsp;UNIQUE(quantity, dose\_measure\_name)  
&emsp;&emsp;IC-71  
&nbsp;  
Medicine(<u>medicine\_id</u>, medicine\_name, active\_ingredient)  
&emsp;&emsp;NOT NULL(medicine\_name)  
&emsp;&emsp;UNIQUE(medicine\_name)  
&emsp;&emsp;IC-149  
&nbsp;  
medicine\_routes(<u>medicine\_id, admin\_route\_id</u>)  
&emsp;&emsp;medicine\_id: FK(Medicine)  
&emsp;&emsp;admin\_route\_id: FK(Administration\_Route)  
&emsp;&emsp;IC-145  
&nbsp;  
Prescription\_Schedule(<u>presc\_schedule\_number</u>)  
&emsp;&emsp;IC-142, IC-143  
&nbsp;  
SOS\_Prescription\_Schedule(<u>presc\_schedule\_number</u>, description)  
&emsp;&emsp;NOT NULL(description)  
&emsp;&emsp;IC-142, IC-143  
Recurrent\_Prescription\_Schedule(<u>presc\_schedule\_number</u>, start\_date, end\_date, frequency, period, presc\_period\_unit)  
&emsp;&emsp;presc\_schedule\_number: FK(Prescription\_Schedule)  
&emsp;&emsp;presc\_period\_unit: ENUM  
&emsp;&emsp;IC-18, IC-56, IC-57, IC-58, IC-89, IC-90, IC-91, IC-92, IC-93, IC-94, IC-95, IC-96, IC-142, IC-143  
&nbsp;  
Non\_Recurrent\_Prescription\_Schedule(<u>presc\_schedule\_number)</u>  
&emsp;&emsp;presc\_schedule\_number: FK(Prescription\_Schedule)  
&emsp;&emsp;IC-142, IC-143  
&nbsp;  
recurrent\_prescription\_schedule\_days\_of\_week(<u>presc\_schedule\_number, day\_of\_week</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Recurrent\_Prescription\_Schedule)  
&emsp;&emsp;day\_of\_week: ENUM  
&emsp;&emsp;IC-1  
&nbsp;  
recurrent\_prescription\_schedule\_months(<u>presc\_schedule\_number, day\_of\_month\_number</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Recurrent\_Prescription\_Schedule)  
&emsp;&emsp;IC-55  
&nbsp;  
recurrent\_prescription\_schedule\_moment(<u>presc\_schedule\_number, moment\_of\_day</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Recurrent\_Prescription\_Schedule)  
&emsp;&emsp;moment\_of\_day: ENUM  
&emsp;&emsp;IC-17  
&nbsp;  
non\_recurrent\_prescription\_schedule\_simple\_dates(<u>presc\_schedule\_number, presc\_date</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Non\_Recurrent\_Prescription\_Schedule)  
&nbsp;  
non\_recurrent\_prescription\_schedule\_moment\_dates(<u>presc\_schedule\_number, presc\_date, moment\_of\_day</u>)  
&emsp;&emsp;presc\_schedule\_number, presc\_date: FK(non\_recurrent\_prescription\_schedule\_simple\_dates)  
&emsp;&emsp;moment\_of\_day: ENUM  
&emsp;&emsp;IC-17  
&nbsp;  
Prescription(<u>prescription\_number</u>, client\_id, medicine\_id, dose\_id, admin\_route\_id, presc\_schedule\_number, id\_who\_regists, regist\_date, id\_who\_cancels, cancel\_date)  
&emsp;&emsp;client\_id: FK(Client)  
&emsp;&emsp;medicine\_id: FK(Medicine)  
&emsp;&emsp;dose\_id: FK(Dose)  
&emsp;&emsp;admin\_route\_id: FK(Administration\_Route)  
&emsp;&emsp;presc\_schedule\_number: FK(Prescription\_Schedule)  
&emsp;&emsp;id\_who\_regists: FK(Collaborator)  
&emsp;&emsp;id\_who\_cancels: FK(Collaborator)  
&emsp;&emsp;NOT NULL(client\_id)  
&emsp;&emsp;NOT NULL(medicine\_id)  
&emsp;&emsp;NOT NULL(dose\_id)  
&emsp;&emsp;NOT NULL(admin\_route\_id)  
&emsp;&emsp;NOT NULL(presc\_schedule\_number)  
&emsp;&emsp;NOT NULL(id\_who\_regists)  
&emsp;&emsp;NOT NULL(regist\_date)  
&emsp;&emsp;IC-87, IC-88, IC-144, IC-147  
&nbsp;  
Medicine\_Administration(<u>med\_admin\_number</u>, med\_admin\_date\_time, client\_id , medicine\_id, dose\_id, observations, coll\_id, prescription\_number, admin\_route\_id)  
&emsp;&emsp;client\_id: FK(Client)  
&emsp;&emsp;medicine\_id: FK(Medicine)  
&emsp;&emsp;dose\_id: FK(Dose)  
&emsp;&emsp;coll\_id: FK(Collaborator)  
&emsp;&emsp;admin\_route\_id: FK(Administration\_Route)  
&emsp;&emsp;prescription\_number: FK(Prescription)  
&emsp;&emsp;medicine\_id, admin\_route\_id: FK(medicine\_routes)  
&emsp;&emsp;NOT NULL(med\_admin\_date\_time)  
&emsp;&emsp;NOT NULL(client\_id)  
&emsp;&emsp;NOT NULL(medicine\_id)  
&emsp;&emsp;NOT NULL(dose\_id)  
&emsp;&emsp;NOT NULL(coll\_id)  
&emsp;&emsp;NOT NULL(admin\_route\_id)  
&emsp;&emsp;UNIQUE(med\_admin\_date\_time, client\_id, medicine\_id)  
&emsp;&emsp;IC-83, IC-84, IC-85, IC-86, IC-148, IC-149, IC-185  
&nbsp;  
&nbsp;  
**\#\# Observations and Occurrence**  
&nbsp;  
Patient\_Observation(<u>observation\_id</u>, patient\_id, coll\_id, created\_at, observed\_at, content)  
&emsp;&emsp;patient\_id: FK(Patient)  
&emsp;&emsp;coll\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(patient\_id)  
&emsp;&emsp;NOT NULL(coll\_id)  
&emsp;&emsp;NOT NULL(created\_at)  
&emsp;&emsp;NOT NULL(observed\_at)  
&emsp;&emsp;NOT NULL(content)  
&emsp;&emsp;IC-137  
&nbsp;  
Patient\_Occurrence\_Category(<u>occ\_category\_id</u>, is\_active)  
&emsp;&emsp;occ\_category\_id: FK(Occurrence\_Category)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-21, IC-148  
&nbsp;  
Child\_Occurrence\_Category(<u>occ\_category\_id</u>, is\_active)  
&emsp;&emsp;occ\_category\_id: FK(Occurrence\_Category)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-22, IC-148  
&nbsp;  
Occurrence(<u>occ\_number</u>, occ\_date\_time, description, coll\_id)  
&emsp;&emsp;coll\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(occ\_date\_time)  
&emsp;&emsp;NOT NULL(coll\_id)  
&emsp;&emsp;C-146, IC-147  
&nbsp;  
Patient\_Occurrence(<u>occ\_number</u>, patient\_id, occ\_category\_id)  
&emsp;&emsp;occ\_number: FK(Occurrence)  
&emsp;&emsp;patient\_id: FK(Patient)  
&emsp;&emsp;occ\_category\_name: FK(Patient\_Occurrence\_Category)  
&emsp;&emsp;NOT NULL(patient\_id)  
&emsp;&emsp;NOT NULL(occ\_category\_id)  
&emsp;&emsp;UNIQUE(patient\_id, occ\_date\_time, occ\_category\_id)  
&emsp;&emsp;IC-146, IC-147, IC-157  
&nbsp;  
Child\_Occurrence(<u>occ\_number</u>, child\_id, occ\_category\_id)  
&emsp;&emsp;occ\_number: FK(Occurrence)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;occ\_category\_name: FK(Child\_Occurrence\_Category)  
&emsp;&emsp;NOT NULL(child\_id)  
&emsp;&emsp;NOT NULL(occ\_category\_id)  
&emsp;&emsp;UNIQUE(child\_id, occ\_date\_time, occ\_category\_id)  
&emsp;&emsp;IC-146, IC-147, IC-167  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Services, Tasks and Visits (Home Care Service and Senior Day Care)**  
&nbsp;  
Care\_Service(<u>care\_service\_id</u>, care\_service\_name, care\_service\_cat\_id)  
&emsp;&emsp;care\_service\_cat\_id: FK(Care\_Service\_Category)  
&emsp;&emsp;NOT NULL(care\_service\_cat)  
&emsp;&emsp;UNIQUE(care\_service\_name)  
&emsp;&emsp;IC-24, IC-151  
&nbsp;  
Home\_Care\_Service(<u>care\_service\_id</u>, is\_active)  
&emsp;&emsp;care\_service\_id: FK(Care\_Service)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-25, IC-151  
&nbsp;  
Day\_Care\_Service(<u>care\_service\_id</u>, is\_active)  
&emsp;&emsp;care\_service\_id: FK(Care\_Service)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-26, IC-151  
&nbsp;  
Biometric\_Service(<u>care\_service\_id</u>, biometric\_unit, primary\_label, secondary\_label)  
care\_service\_id: FK(Care\_Service)  
NOT NULL(biometric\_unit)  
NOT NULL(primary\_label)  
IC-151, IC-189  
&nbsp;  
home\_care\_patient\_service\_list(<u>patient\_service\_id</u>, patient\_id, care\_service\_id, day\_of\_week, valid\_since, valid\_until)  
&emsp;&emsp;patient\_id: FK(Home\_Care\_Patient)  
&emsp;&emsp;care\_service\_id: FK(Home\_Care\_Service)  
&emsp;&emsp;UNIQUE(patient\_id, care\_service\_id, day\_of\_week, valid\_since)  
&emsp;&emsp;day\_of\_week: ENUM  
&emsp;&emsp;IC-1, IC-49, IC-72, IC-85  
&nbsp;  
day\_care\_patient\_service\_list(<u>patient\_service\_id</u>, patient\_id, care\_service\_id, day\_of\_week, valid\_since, valid\_until)  
&emsp;&emsp;patient\_id: FK(Day\_Care\_Patient)  
&emsp;&emsp;care\_service\_id: FK(Day\_Care\_Service)  
&emsp;&emsp;UNIQUE(patient\_id, care\_service\_id, day\_of\_week, valid\_since)  
&emsp;&emsp;day\_of\_week: ENUM  
&emsp;&emsp;IC-1, IC-49, IC-72, IC-84  
&nbsp;  
Visit(<u>visit\_number</u>, visit\_date, arrival\_time, patient\_id, departure\_time, patient\_signature\_path, observations)  
&emsp;&emsp;patient\_id: FK(Home\_Care\_Patient)  
&emsp;&emsp;NOT NULL(visit\_date)  
&emsp;&emsp;NOT NULL(arrival\_time)  
&emsp;&emsp;NOT NULL(patient\_id)  
&emsp;&emsp;NOT NULL(departure\_time)  
&emsp;&emsp;NOT NULL(patient\_signature\_path)  
&emsp;&emsp;UNIQUE(visit\_date, arrival\_time, id)  
&emsp;&emsp;IC-59, IC-159  
&nbsp;  
visit\_services(<u>visit\_number, care\_service\_id</u>)  
&emsp;&emsp;visit\_number: FK(Visit)  
&emsp;&emsp;care\_service\_id: FK(Home\_Care\_Service)  
&nbsp;  
visit\_collaborators(<u>visit\_number, coll\_id</u>)  
&emsp;&emsp;visit\_number: FK(Visit)  
&emsp;&emsp;coll\_id: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;IC-149  
&nbsp;  
&nbsp;  
Care\_Task(<u>task\_number</u>, patient\_id, task\_timestamp, observations, coll\_id, care\_service\_id)  
&emsp;&emsp;patient\_id: FK(Day\_Care\_Patient)  
&emsp;&emsp;coll\_id: FK(Day\_Care\_Collaborator)  
&emsp;&emsp;care\_service\_id: FK(Day\_Care\_Service)  
&emsp;&emsp;NOT NULL(patient\_id)  
&emsp;&emsp;NOT NULL(task\_timestamp)  
&emsp;&emsp;NOT NULL(coll\_id)  
&emsp;&emsp;NOT NULL(care\_service\_id)  
&emsp;&emsp;UNIQUE(patient\_id, task\_timestamp, care\_service\_id)  
&emsp;&emsp;IC-150, IC-158  
&nbsp;  
Biometric\_Task(<u>task\_number</u>, biometric\_value, biometric\_value\_secondary)  
&emsp;&emsp;task\_number: FK(Care\_Task)  
&emsp;&emsp;NOT NULL(task\_number)  
&emsp;&emsp;NOT NULL(biometric\_value)  
&emsp;&emsp;IC-150, IC-187, IC-188  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Zones, Shifts and Requests (Home Care Service Specific)**  
&nbsp;  
Zone(<u>zone\_id</u>, zone\_name, min\_collab, is\_active)  
&emsp;&emsp;NOT NULL(zone\_name)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;UNIQUE(zone\_name)  
&emsp;&emsp;IC-27  
&nbsp;  
Zone\_Hours(<u>zone\_hours\_id</u>, start\_time, start\_break\_time, end\_break\_time, end\_time)  
&emsp;&emsp;NOT NULL(start\_time)  
&emsp;&emsp;NOT NULL(start\_break\_time)  
&emsp;&emsp;NOT NULL(end\_break\_time)  
&emsp;&emsp;NOT NULL(end\_time)  
&emsp;&emsp;UNIQUE(start\_time, start\_break\_time, end\_break\_time, end\_time)  
&emsp;&emsp;IC-28, IC-61
  
Holiday(<u>holiday\_id</u>, holiday\_date, holiday\_name, is\_working\_holiday)  
&emsp;&emsp;NOT NULL(holiday\_date)  
&emsp;&emsp;NOT NULL(holiday\_name)  
&emsp;&emsp;NOT NULL(is\_working\_holiday)  
&emsp;&emsp;UNIQUE(holiday\_date)  
&nbsp;  
zone\_schedule\_hours(<u>zone\_id, zone\_hours\_id, valid\_since</u>, valid\_until)  
&emsp;&emsp;zone\_id: FK(Zone)  
&emsp;&emsp;zone\_hours\_id: FK(Zone\_Hours)  
&emsp;&emsp;IC-30, IC-49, IC-72, IC-153  
&nbsp;  
zone\_schedule\_week(<u>zone\_id, day\_of\_week, valid\_since</u>, valid\_until)  
&emsp;&emsp;zone\_id: FK(Zone)  
&emsp;&emsp;day\_of\_week: ENUM  
&emsp;&emsp;IC-1, IC-29, IC-49, IC-72  
&nbsp;  
holiday\_zone\_availability(<u>holiday\_id, zone\_id</u>)  
&emsp;&emsp;holiday\_id: FK(Holiday)  
&emsp;&emsp;zone\_id: FK(Zone)  
&emsp;&emsp;IC-99  
&nbsp;  
zone\_patient\_list(<u>zone\_id, patient\_id, valid\_since</u>, valid\_until, visit\_order)  
&emsp;&emsp;zone\_id: FK(Zone)  
&emsp;&emsp;patient\_id: FK(Home\_Care\_Patient)  
&emsp;&emsp;IC-49, IC-60, IC-72, IC-97  
&nbsp;  
Shift\_Schedule\_Period(<u>shift\_schedule\_period\_id,</u>&nbsp;start\_date, end\_date, is\_published,&nbsp;admin\_id)  
&emsp;&emsp;admin\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(start\_date)  
&emsp;&emsp;NOT NULL(end\_date)  
&emsp;&emsp;NOT NULL(is\_published)  
&emsp;&emsp;NOT NULL(admin\_id)  
&emsp;&emsp;IC-58, IC-100  
&nbsp;  
Schedule\_Job(<u>job\_number</u>, shift\_schedule\_period\_id, admin\_id, requested\_date\_time, status, error\_message)  
&emsp;&emsp;shift\_schedule\_period\_id: FK(Shift\_Schedule\_Period)  
&emsp;&emsp;admin\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(shift\_schedule\_period\_id)  
&emsp;&emsp;NOT NULL(admin\_id)  
&emsp;&emsp;NOT NULL(requested\_date\_time)  
&emsp;&emsp;NOT NULL(status)  
&emsp;&emsp;IC-63  
&nbsp;  
Shift(<u>shift\_id,</u>&nbsp;zone\_id, date, shift\_schedule\_period\_id)  
&emsp;&emsp;zone\_id: FK(Zone)  
&emsp;&emsp;shift\_schedule\_period\_id: FK(Shift\_Schedule\_Period)  
&emsp;&emsp;UNIQUE(zone\_id, date)  
&emsp;&emsp;NOT NULL(shift\_schedule\_period\_id)  
&emsp;&emsp;NOT NULL(zone\_id)  
&emsp;&emsp;NOT NULL(date)  
&emsp;&emsp;IC-101  
&nbsp;  
shift\_assignment(<u>shift\_assignment\_id</u>, shift\_id, coll\_id)  
&emsp;&emsp;shift\_id: FK(Shift)  
&emsp;&emsp;coll\_id: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;UNIQUE(shift\_id,&nbsp;coll\_id)  
&emsp;&emsp;NOT NULL(shift\_id)  
&emsp;&emsp;NOT NULL(coll\_id)  
&emsp;&emsp;IC-98, IC-102, IC-103, IC-104, IC-105  
&nbsp;  
Request(<u>request\_number,</u>&nbsp;coll\_id, date\_time, is\_expired, admin\_id, is\_approved, approval\_date\_time)  
&emsp;&emsp;coll\_id: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;admin\_id: FK(Collaborator)  
&emsp;&emsp;UNIQUE(coll\_id, date\_time)  
&emsp;&emsp;NOT NULL(coll\_id)  
&emsp;&emsp;NOT NULL(date\_time)  
&emsp;&emsp;NOT NULL(is\_expired)  
&emsp;&emsp;IC-152, IC-154, IC-155  
&nbsp;  
Absence(<u>request\_number</u>, start\_date, end\_date, justification\_text)  
&emsp;&emsp;request\_number: FK(Request)  
&emsp;&emsp;NOT NULL(start\_date)  
&emsp;&emsp;NOT NULL(end\_date)  
&emsp;&emsp;NOT NULL(justification\_text)  
&emsp;&emsp;IC-154, IC-155  
&nbsp;  
Vacation(<u>request\_number</u>, start\_date, end\_date, comment\_text)  
&emsp;&emsp;request\_number: FK(Request)  
&emsp;&emsp;NOT NULL(start\_date)  
&emsp;&emsp;NOT NULL(end\_date)  
&emsp;&emsp;IC-58, IC-154, IC-155  
&nbsp;  
Time\_Off\_Swap(<u>request\_number</u><u>,</u>&nbsp;original\_date, requested\_date, comment\_text)  
&emsp;&emsp;request\_number: FK(Request)  
&emsp;&emsp;NOT NULL(original\_date)  
&emsp;&emsp;NOT NULL(requested\_date)  
&emsp;&emsp;IC-62, IC-154, IC-155  
&nbsp;  
Shift\_Swap(<u>request\_number</u>, from\_shift\_assignment\_id, to\_shift\_assignment\_id, comment\_text, is\_accepted, acceptance\_date\_time)  
&emsp;&emsp;request\_number: FK(Request)  
&emsp;&emsp;from\_shift\_assignment\_id: FK(shift\_assignment)  
&emsp;&emsp;to\_shift\_assignment\_id: FK(shift\_assignment)  
&emsp;&emsp;NOT NULL(from\_shift\_assignment\_id)  
&emsp;&emsp;IC-64, IC-106, IC-107, IC-108, IC-109, IC-154, IC-155  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Child Specifics**  
&nbsp;  
Feeding(<u>id</u>, child\_id, auxiliar\_id, occurred\_at, is\_lunch, observations)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;auxiliar\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(is\_lunch)  
&emsp;&emsp;NOT NULL(auxiliar\_id)  
&emsp;&emsp;NOT NULL(occurred\_at)  
&emsp;&emsp;UNIQUE(child\_id, occurred\_at)  
&emsp;&emsp;IC-156  
&nbsp;  
Hygiene(<u>id</u>, child\_id, occurred\_at, auxiliar\_id, hygiene\_type)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;auxiliar\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL (auxiliar\_id)  
&emsp;&emsp;NOT NULL (type)  
&emsp;&emsp;NOT NULL(hygiene\_type)  
&emsp;&emsp;UNIQUE(child\_id, occurred\_at)  
&emsp;&emsp;IC-32,&nbsp;IC-157  
&nbsp;  
Attendance(<u>id</u>, child\_id, occurred\_at, auxiliar\_id, companion\_id, is\_entry)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;auxiliar\_id: FK(Collaborator)  
&emsp;&emsp;companion\_id: FK(Person)  
&emsp;&emsp;NOT NULL(auxiliar\_id)  
&emsp;&emsp;NOT NULL(is\_entry)  
&emsp;&emsp;NOT NULL(occurred\_at)  
&emsp;&emsp;UNIQUE(child\_id, occurred\_at)  
&emsp;&emsp;IC-65,&nbsp;IC-158, IC-177, IC-178  
&nbsp;  
Activity\_Session(<u>id</u>, activity\_id, auxiliar\_id, date, is\_in\_the\_morning,&nbsp;description)  
&emsp;&emsp;auxiliar\_id: FK(Collaborator)  
&emsp;&emsp;activity\_id: FK(Activity)  
&emsp;&emsp;NOT NULL(auxiliar\_id)  
&emsp;&emsp;NOT NULL(date)  
&emsp;&emsp;UNIQUE&nbsp;(date, is\_in\_the\_morning,&nbsp;activity\_id)  
&nbsp;  
Activity(<u>id</u>, name)  
&emsp;&emsp;NOT NULL(name)  
&emsp;&emsp;UNIQUE(name)  
&nbsp;  
child\_activity(<u>id</u>, child\_id, session\_id, individual\_notes)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;session\_id: FK(Activity\_Session)  
&emsp;&emsp;UNIQUE(child\_id, session\_id)  
&nbsp;  
Photo(i<u>d</u>, session\_id, auxiliar\_id, file\_path, caption, upload\_time)  
&emsp;&emsp;auxiliar\_id: FK(Collaborator)  
&emsp;&emsp;session\_id : FK(Activity\_Session)  
&emsp;&emsp;NOT NULL(auxiliar\_id)  
&emsp;&emsp;NOT NULL(file\_path)  
&emsp;&emsp;IC-110, IC-115  
&nbsp;  
child\_photo(<u>photo\_id, child\_id</u>)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;photo\_id: FK(Photo)  
&emsp;&emsp;UNIQUE(photo\_id, child\_id)  
&emsp;&emsp;IC-114  
&nbsp;  
Authorization\_Form<u>(id</u>, child\_id, authorized\_person\_id, guardian\_id, educator\_id, valid\_since, valid\_until, status, relationship)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;authorized\_person\_id: FK(Person)  
&emsp;&emsp;guardian\_id: FK(Guardian)  
&emsp;&emsp;educator\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(guardian\_id)  
&emsp;&emsp;NOT NULL(valid\_since)  
&emsp;&emsp;NOT NULL(valid\_until)  
&emsp;&emsp;NOT NULL(status)  
&emsp;&emsp;NOT NULL(relationship)  
&emsp;&emsp;UNIQUE&nbsp;(child\_id, authorized\_person\_id,&nbsp;valid\_since)  
&emsp;&emsp;IC-33, IC-49, IC-72, IC-116, IC-161, IC-162, IC-180  
&nbsp;  
&nbsp;  
Pedagogical\_Evaluation(<u>id</u>, child\_id, created\_at, educator\_id)  
&emsp;&emsp;educator\_id: FK(Collaborator)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;NOT NULL(educator\_id)  
&emsp;&emsp;NOT NULL(created\_at)  
&emsp;&emsp;UNIQUE(child\_id, created\_at)  
&emsp;&emsp;IC-159  
&nbsp;  
&nbsp;  
Evaluation\_Theme(<u>id</u>, evaluation\_id, category\_id, objectives, actions, resources, assessment)  
&emsp;&emsp;evaluation\_id: FK(Pedagogical\_Evaluation)  
&emsp;&emsp;category\_id: FK(Evaluation\_Category)  
&emsp;&emsp;UNIQUE(child\_id, theme\_id)  
&nbsp;  
&nbsp;  
Individual\_Educational\_Plan(<u>id</u>, child\_id, created\_at, educator\_id)  
&emsp;&emsp;child\_id: FK(Child)  
&emsp;&emsp;educator\_id: FK(Collaborator)  
&emsp;&emsp;NOT NULL(educator\_id)  
&emsp;&emsp;UNIQUE(child\_id, created\_at)  
&emsp;&emsp;IC-160  
&nbsp;  
Evaluation\_Category(<u>id</u>, name,  is\_active)  
&emsp;&emsp;NOT NULL(name)  
&emsp;&emsp;UNIQUE(name)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-37, IC-111,&nbsp;IC-164  
&nbsp;  
Evaluation\_Subcategory(<u>id</u>, category\_id, name, is\_active)  
&emsp;&emsp;category\_id: FK(Evaluation\_Category)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;NOT NULL(name)  
&emsp;&emsp;UNIQUE(category\_id, name)  
&emsp;&emsp;IC-38, IC-39, IC-112,&nbsp;IC-163  
&nbsp;  
&nbsp;  
Milestone(<u>id</u>, name, subcategory\_id, is\_active, description, age\_group)  
&emsp;&emsp;subcategory\_id: FK(Evaluation\_Subcategory)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;NOT NULL(name)  
&emsp;&emsp;age\_group: Enum  
&emsp;&emsp;UNIQUE(subcategory\_id, name, age\_group)  
&emsp;&emsp;IC-31, IC-40,&nbsp;IC-41  
&nbsp;  
plan\_milestone\_status(<u>plan\_id, milestone\_id</u>, measure\_label)  
&emsp;&emsp;plan\_id: FK(Individual\_Evaluation\_Plan)  
&emsp;&emsp;milestone\_id: FK(Milestone)  
&emsp;&emsp;NOT NULL(measure\_label)  
&emsp;&emsp;UNIQUE(plan\_id, milestone\_id)  
&emsp;&emsp;IC-34, IC-113, IC-181  
&nbsp;  
&nbsp;  
**\#\# Assets**  
&nbsp;  
Supplier(<u>id</u>, name, nif, fiscal\_address, supply\_address, business\_sector, contact\_person\_name, mobile\_phone, landline\_phone, primary\_email, secondary\_email, supplier\_created\_date, bank\_name, iban, swift\_code, internal\_supplier\_rating, important\_notes, general\_notes)  
&nbsp;  
&emsp;&emsp;NOT NULL(name)  
&nbsp;  
&emsp;&emsp;NOT NULL(NIF)  
&nbsp;  
&emsp;&emsp;NOT NULL(fiscal\_address)  
&nbsp;  
&emsp;&emsp;NOT NULL(supply\_address)  
&nbsp;  
&emsp;&emsp;NOT NULL(business\_sector)  
&nbsp;  
&emsp;&emsp;NOT NULL(contact\_person\_name)  
&nbsp;  
&emsp;&emsp;NOT NULL(mobile\_phone)  
&nbsp;  
&emsp;&emsp;NOT NULL(landline\_phone)  
&nbsp;  
&emsp;&emsp;NOT NULL(primary\_email)  
&nbsp;  
&emsp;&emsp;NOT NULL(secondary\_email)  
&nbsp;  
&emsp;&emsp;NOT NULL(supplier\_created\_date)  
&nbsp;  
&emsp;&emsp;NOT NULL(bank\_name)  
&nbsp;  
&emsp;&emsp;NOT NULL(iban)  
&nbsp;  
&emsp;&emsp;NOT NULL(swift\_code)  
&nbsp;  
&emsp;&emsp;NOT NULL(internal\_supplier\_rating)  
&nbsp;  
&emsp;&emsp;important\_notes  
&nbsp;  
&emsp;&emsp;general\_notes  
&nbsp;  
&emsp;&emsp;UNIQUE(nif)  
Asset\_Location(<u>asset\_location\_id</u>, asset\_location\_name)  
&emsp;&emsp;NOT NULL(asset\_location\_name)  
&emsp;&emsp;UNIQUE(asset\_location\_name)  
&emsp;&emsp;IC-42  
&nbsp;  
Asset\_Category(<u>asset\_category\_id</u>, asset\_category\_name)  
&emsp;&emsp;NOT NULL(asset\_category\_name)  
&emsp;&emsp;UNIQUE(asset\_category\_name)  
&emsp;&emsp;IC-45  
&nbsp;  
&nbsp;  
Asset(<u>id</u>, asset\_code, is\_active, disposal\_date, location, technical\_characteristics, acquisition\_date, service\_start\_date, acquisition\_cost, designation, supplier\_id, asset\_category\_id)  
&nbsp;  
&emsp;&emsp;NOT NULL(asset\_code)  
&nbsp;  
&emsp;&emsp;NOT NULL(is\_active)  
&nbsp;  
&emsp;&emsp;NOT NULL(disposal\_date)  
&nbsp;  
&emsp;&emsp;asset\_location\_id: FK(Asset\_Location)  
&nbsp;  
&emsp;&emsp;NOT NULL(technical\_characteristics)  
&nbsp;  
&emsp;&emsp;NOT NULL(acquisition\_date)  
&nbsp;  
&emsp;&emsp;NOT NULL(service\_start\_date)  
&nbsp;  
&emsp;&emsp;NOT NULL(acquisition\_cost)  
&nbsp;  
&emsp;&emsp;NOT NULL(designation)  
&nbsp;  
&emsp;&emsp;supplier\_id: FK(Supplier)  
&nbsp;  
&emsp;&emsp;asset\_category\_id: FK(Asset\_Category)  
&nbsp;  
&emsp;&emsp;asset\_category\_name: ENUM  
&nbsp;  
&emsp;&emsp;UNIQUE(asset\_code)  
&nbsp;  
&emsp;&emsp;IC-42, IC-119, IC-120, IC-167, IC-168, IC-169  
&nbsp;  
Intervention\_Status(<u>status\_id</u>, status\_name)  
&emsp;&emsp;NOT NULL(status\_name)  
&emsp;&emsp;UNIQUE(status\_name)  
&emsp;&emsp;IC-43  
&nbsp;  
Intervention\_Category(<u>intervention\_category\_id</u>, intervention\_category\_name)  
&emsp;&emsp;NOT NULL(intervention\_category\_name)  
&emsp;&emsp;UNIQUE(intervention\_category\_name)  
&emsp;&emsp;IC-44  
&nbsp;  
Expense\_Type(<u>expense\_type\_id</u>, expense\_type\_name)  
&emsp;&emsp;NOT NULL(expense\_type\_name)  
&emsp;&emsp;UNIQUE(expense\_type\_name)  
&emsp;&emsp;IC-46  
&nbsp;  
&nbsp;  
Intervention(<u>id</u>, asset\_id, intervention\_date, description, status\_id, intervention\_category\_id, id\_who\_regists)  
&nbsp;  
&emsp;&emsp;asset\_id: FK(Asset)  
&nbsp;  
&emsp;&emsp;NOT NULL(intervention\_date)  
&nbsp;  
&emsp;&emsp;NOT NULL(description)  
&nbsp;  
&emsp;&emsp;status\_id: FK(Intervention\_Status)  
&emsp;&emsp;intervention\_category\_id: FK(Intervention\_Category)  
&emsp;&emsp;id\_who\_regists: FK(Collaborator)  
&nbsp;  
&emsp;&emsp;UNIQUE(asset\_id, intervention\_date)  
&nbsp;  
&emsp;&emsp;IC-121, IC-125, IC-126, IC-127, IC-128, IC-131, IC-165, IC-166, IC-167  
&nbsp;  
Email(<u>id</u>, asset\_id, date\_time, subject, storage\_path, id\_who\_upload)  
&nbsp;  
&emsp;&emsp;asset\_id: FK(Asset)  
&nbsp;  
&emsp;&emsp;NOT NULL(date\_time)  
&nbsp;  
&emsp;&emsp;NOT NULL(subject)  
&nbsp;  
&emsp;&emsp;NOT NULL(storage\_path)  
&nbsp;  
&emsp;&emsp;id\_who\_upload: FK(Collaborator)  
&nbsp;  
&emsp;&emsp;UNIQUE(asset\_id, date\_time)  
&nbsp;  
&emsp;&emsp;IC-66, IC-117, IC-168, IC-170, IC-172, IC-174  
&nbsp;  
&nbsp;  
Document(<u>id</u>, asset\_id, date, filename, file\_path)  
&nbsp;  
&emsp;&emsp;asset\_id: FK(Asset)  
&nbsp;  
&emsp;&emsp;NOT NULL(date)  
&nbsp;  
&emsp;&emsp;NOT NULL(filename)  
&nbsp;  
&emsp;&emsp;NOT NULL(file\_path)  
&nbsp;  
&emsp;&emsp;UNIQUE(asset\_id, date)  
&nbsp;  
&emsp;&emsp;IC-67, IC-124, IC-129, IC-169, IC-171, IC-173, IC-174  
&nbsp;  
&nbsp;  
&nbsp;  
Normal\_Document(<u>document\_id</u>)  
&nbsp;  
&emsp;&emsp;document\_id: FK(Document)  
&nbsp;  
&nbsp;  
Expense\_Document(<u>document\_id</u>, expense\_id)  
&nbsp;  
&emsp;&emsp;document\_id: FK(Document)  
&nbsp;  
&emsp;&emsp;expense\_id: FK(Expense)  
&nbsp;  
&emsp;&emsp;NOT NULL(expense\_id)  
&nbsp;  
&nbsp;  
Intervention\_Document(<u>document\_id</u>, intervention\_id)  
&nbsp;  
&emsp;&emsp;document\_id: FK(Document)  
&nbsp;  
&emsp;&emsp;intervention\_id: FK(Intervention)  
&nbsp;  
&emsp;&emsp;NOT NULL(intervention\_id)  
&nbsp;  
&nbsp;  
Email\_Document(<u>email\_id, document\_id</u>)  
&nbsp;  
&emsp;&emsp;email\_id: FK(Email)  
&nbsp;  
&emsp;&emsp;document\_id: FK(Document)  
&nbsp;  
&emsp;&emsp;IC-170, IC-171, IC-172, IC-173, IC-174  
&nbsp;  
&nbsp;  
Expense(<u>id</u>, intervention\_id, date, description, associated\_cost, expense\_type\_id)  
&nbsp;  
&emsp;&emsp;intervention\_id: FK(Intervention)  
&nbsp;  
&emsp;&emsp;NOT NULL(date)  
&nbsp;  
&emsp;&emsp;NOT NULL(description)  
&nbsp;  
&emsp;&emsp;NOT NULL(associated\_cost)  
&nbsp;  
&emsp;&emsp;expense\_type\_id: FK(Expense\_Type)  
&nbsp;  
&emsp;&emsp;IC-123, IC-165  
&nbsp;  
&nbsp;  
Alert(<u>id</u>, intervention\_id, alert\_date, advance\_notification\_period)  
&nbsp;  
&emsp;&emsp;intervention\_id: FK(Intervention)  
&nbsp;  
&emsp;&emsp;NOT NULL(alert\_date)  
&nbsp;  
&emsp;&emsp;NOT NULL(advance\_notification\_period)  
&nbsp;  
&emsp;&emsp;IC-118, IC-122, IC-130, IC-166  
