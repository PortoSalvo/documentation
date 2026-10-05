# Direct Relational Model

This model is a direct translation of the Enterprise Architect (EA) conceptual model into relational form, with no further optimization applied.

&nbsp;  
&nbsp;  
**\#\# Global Entities**  
&nbsp;  
Validation\_Period(<u>valid\_since, valid\_until</u>)  
&emsp;&emsp;IC-49  
&nbsp;  
Day\_of\_Week(<u>day\_of\_week\_name</u>)  
&emsp;&emsp;day\_of\_week\_name: ENUM  
&emsp;&emsp;IC-1  
&nbsp;  
&nbsp;  
**\#\# Users, Roles and Permissions**  
&nbsp;  
Domain(<u>domain\_name</u>)  
&emsp;&emsp;IC-3  
&nbsp;  
Object(<u>object\_name</u>, domain\_name)  
&emsp;&emsp;domain\_name: FK(Domain)  
&emsp;&emsp;NOT NULL(domain\_name)  
&emsp;&emsp;IC-4  
&nbsp;  
Operation(<u>operation\_name</u>)  
&emsp;&emsp;operation\_name: ENUM  
&emsp;&emsp;IC-2  
&nbsp;  
Role(<u>role\_name</u>, description)  
&emsp;&emsp;IC-5  
&nbsp;  
role\_domains(<u>role\_name, domain\_name</u>, is\_admin)  
&emsp;&emsp;role\_name: FK(Role)  
&emsp;&emsp;domain\_name: FK(Domain)  
&emsp;&emsp;NOT NULL(is\_admin)  
&emsp;&emsp;IC-5  
&nbsp;  
role\_permissions(<u>role\_name, operation\_name, object\_name</u>)  
&emsp;&emsp;role\_name: FK(Role)  
&emsp;&emsp;operation\_name: FK(Operation)  
&emsp;&emsp;object\_name: FK(Object)  
&emsp;&emsp;IC-6  
&nbsp;  
User(<u>username</u>, password, is\_active, email)  
&emsp;&emsp;NOT NULL(password)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;UNIQUE(email)  
&emsp;&emsp;IC-74, IC-75, IC-190  
&nbsp;  
user\_roles(<u>username, role\_name</u>)  
&emsp;&emsp;username: FK(User)  
&emsp;&emsp;role\_name: FK(Role)  
&emsp;&emsp;IC-133  
&nbsp;  
&nbsp;  
**\#\# Person Hierarchy (and close relations)**  
Phone(<u>phone\_number</u>)  
&emsp;&emsp;IC-52  
&nbsp;  
Person(<u>cc</u>, name, gender, birth\_date, email, address\_line\_1, address\_line\_2, city, country, zipcode, profile\_image\_path)  
&emsp;&emsp;NOT NULL(name)  
&emsp;&emsp;NOT NULL(gender)  
&emsp;&emsp;NOT NULL(birth\_date)  
&emsp;&emsp;NOT NULL(address\_line\_1)  
&emsp;&emsp;NOT NULL(city)  
&emsp;&emsp;NOT NULL(country)  
&emsp;&emsp;NOT NULL(zipcode)  
&emsp;&emsp;NOT NULL(profile\_image\_path)  
&emsp;&emsp;gender: ENUM  
&emsp;&emsp;IC-7, IC-51, IC-75, IC-76, IC-134, IC-170, IC-216, IC-217, IC-218  
&nbsp;  
person\_phone\_number(<u>cc, phone\_number</u>)  
&emsp;&emsp;cc: FK(Person)  
&emsp;&emsp;phone\_number: FK(Phone)  
&emsp;&emsp;IC-77, IC-78  
&nbsp;  
Senior\_Reference(<u>cc</u>)  
&emsp;&emsp;cc: FK(Person)  
&emsp;&emsp;IC-134  
&nbsp;  
Guardian(<u>cc</u>, username)  
&emsp;&emsp;cc: FK(Person)  
&emsp;&emsp;username: FK(User)  
&emsp;&emsp;NOT NULL(username)  
&emsp;&emsp;IC-74, IC-75, IC-80, IC-134  
&nbsp;  
Collaborator(<u>cc</u>, username, is\_active)  
&emsp;&emsp;cc: FK(Person)  
&emsp;&emsp;username: FK(User)  
&emsp;&emsp;NOT NULL(username)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-74, IC-75, IC-134, IC-135  
&nbsp;  
Home\_Care\_Collaborator(<u>cc</u>, max\_consecutive\_days, weekly\_hours, rating, is\_active)  
&emsp;&emsp;cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(max\_consecutive\_days)  
&emsp;&emsp;NOT NULL(weekly\_hours)  
&emsp;&emsp;NOT NULL(rating)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-53, IC-54, IC-55, IC-135, IC-159  
&nbsp;  
Day\_Care\_Collaborator(<u>cc</u>, is\_active)  
&emsp;&emsp;cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-135, IC-193  
&nbsp;  
home\_care\_collaborator\_timeoff\_preference(<u>cc</u>, option\_name)  
&emsp;&emsp;cc: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;option\_name: FK(Time\_off)  
&nbsp;  
Time\_off(<u>option\_name</u>)  
&emsp;&emsp;IC-8  
&nbsp;  
time\_off\_days(<u>option\_name, day\_of\_week\_name</u>)  
&emsp;&emsp;option\_name: FK(Time\_off)  
&emsp;&emsp;day\_of\_week\_name: FK(Day\_Of\_Week)  
&emsp;&emsp;IC-81  
&nbsp;  
Client(<u>cc</u>)  
&emsp;&emsp;cc: FK(Person)  
&emsp;&emsp;IC-134, IC-136, IC-137, IC-138  
&nbsp;  
Dietary\_Preference(<u>dietary\_pref\_</u><u>description</u>)  
&nbsp;  
client\_dietary\_preference(<u>cc,</u>&nbsp;<u>dietary\_pref\_</u><u>description</u>)  
&emsp;&emsp;cc: FK(Client)  
&emsp;&emsp;dietary\_pref\_description: FK(Dietary\_Preference)  
&nbsp;  
Religious\_Belief(<u>religion\_name</u>)  
&nbsp;  
client\_religious\_belief(<u>cc, religion\_name</u>)  
&emsp;&emsp;cc: FK(Client)  
&emsp;&emsp;religion\_name: FK(Religious\_Belief)  
&nbsp;  
Meal\_Type(<u>meal\_type\_name</u>)  
&emsp;&emsp;meal\_type\_name: ENUM  
&emsp;&emsp;IC-9  
&nbsp;  
Meal\_Subtype(<u>meal\_subtype\_name</u>)  
&emsp;&emsp;meal\_subtype\_name: ENUM  
&emsp;&emsp;IC-10  
&nbsp;  
Feeding\_Dependency(<u>feeding\_dep\_name</u>)  
&emsp;&emsp;feeding\_dep\_name: ENUM  
&emsp;&emsp;IC-11  
&nbsp;  
Age\_Group(group\_name)  
&emsp;&emsp;PK(group\_name)  
&emsp;&emsp;group\_name: ENUM  
&emsp;&emsp;IC-32  
&nbsp;  
Child(<u>cc</u>, student\_number, classroom, photo\_consent, is\_active, group\_name, guardian\_cc, relationship)  
&emsp;&emsp;cc: FK(Client)  
&emsp;&emsp;group\_name: FK(Age\_Group)  
&emsp;&emsp;guardian\_cc: FK(Guardian)  
&emsp;&emsp;UNIQUE(student\_number)  
&emsp;&emsp;NOT NULL(student\_number)  
&emsp;&emsp;NOT NULL(photo\_consent)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;NOT NULL(guardian\_cc)  
&emsp;&emsp;IC-36, IC-75, IC-136, IC-137, IC-142, IC-163, IC-164, IC-165, IC-166, IC-167, IC-168, IC-169, IC-187, IC-192  
&nbsp;  
Patient(<u>cc</u>,&nbsp;feeding\_dep\_name, meal\_type\_name, meal\_subtype\_name)  
&emsp;&emsp;cc: FK(Client)  
&emsp;&emsp;feeding\_dep\_name: FK(Feeding\_Dependency)  
&emsp;&emsp;meal\_type\_name: FK(Meal\_Type)  
&emsp;&emsp;Meal\_subtype\_name: FK(Meal\_Subtype)  
&emsp;&emsp;IC-82,&nbsp;IC-83, IC-136, IC-137, IC-139, IC-140, IC-143, IC-144, IC-153  
&nbsp;  
Home\_Care\_Patient(<u>cc</u>, is\_active)  
&emsp;&emsp;cc: FK(Patient)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-85, IC-139, IC-140, IC-155  
&nbsp;  
Day\_Care\_Patient(<u>cc</u>, is\_active, process\_number, admission\_date)  
&emsp;&emsp;cc: FK(Patient)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;NOT NULL(process\_number)  
&emsp;&emsp;NOT NULL(admission\_date)  
&emsp;&emsp;UNIQUE(process\_number)  
&emsp;&emsp;IC-84, IC-139, IC-140, IC-154  
&nbsp;  
senior\_reference\_looks\_after\_patient(<u>senior\_ref\_cc, patient\_cc</u>, relationship)  
&emsp;&emsp;senior\_ref\_cc: FK(Senior\_Reference)  
&emsp;&emsp;patient\_cc: FK(Patient)  
&emsp;&emsp;IC-79, IC-141  
&nbsp;  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Patient Autonomy and Health Condition (Senior Day Care and Home Care Service Specific)**  
&nbsp;  
Autonomy\_Dependence\_Level(<u>autonomy\_dep\_level</u>)  
&emsp;&emsp;autonomy\_dep\_level: ENUM  
&emsp;&emsp;IC-12  
&nbsp;  
&nbsp;  
Autonomy\_Category(<u>autonomy\_cat\_</u><u>name</u>)  
&emsp;&emsp;autonomy\_cat\_name: ENUM  
&emsp;&emsp;IC-13  
&nbsp;  
&nbsp;  
Autonomy(<u>aut\_name</u>,&nbsp;autonomy\_cat\_name)  
&emsp;&emsp;autonomy\_cat\_name: FK(Autonomy\_Category)  
&emsp;&emsp;NOT NULL(autonomy\_cat\_name)  
&emsp;&emsp;IC-14  
&nbsp;  
&nbsp;  
patient\_autonomy\_dependence(<u>cc, aut\_</u><u>name,</u>&nbsp;<u>autonomy\_dep\_level</u><u>, valid\_since, valid\_until</u>)  
&emsp;&emsp;cc: FK(Patient)  
&emsp;&emsp;aut\_name: FK(Autonomy)  
&emsp;&emsp;valid\_since, valid\_until: FK(Validation\_Period)  
&emsp;&emsp;IC-73  
&nbsp;  
Health\_Condition\_Category(<u>health\_cat\_</u><u>name</u>)  
&emsp;&emsp;health\_cat\_name: ENUM  
&emsp;&emsp;IC-15  
&nbsp;  
Health\_Condition(<u>health\_cond\_name</u>,&nbsp;health\_cat\_label)  
&emsp;&emsp;health\_cat\_label: FK(Health\_Condition\_Category)  
&emsp;&emsp;NOT NULL(health\_cat\_label)  
&emsp;&emsp;IC-16  
&nbsp;  
client\_health\_cond(<u>cc, health\_cond\_name, valid\_since, valid\_until</u>,&nbsp;observations)  
&emsp;&emsp;cc: FK(Client)  
&emsp;&emsp;health\_cond\_name: FK(Health\_Condition)  
&emsp;&emsp;valid\_since, valid\_until: FK(Validation\_Period)  
&emsp;&emsp;IC-73  
&nbsp;  
&nbsp;  
**\#\# Prescriptions and Medicine\_Administration**  
&nbsp;  
Dose\_Measure(<u>dose\_measure\_name</u>)  
&emsp;&emsp;dose\_measure\_name: ENUM  
&emsp;&emsp;IC-48  
&nbsp;  
Dose(<u>dose\_id</u>, dose\_measure\_name, quantity)  
&emsp;&emsp;dose\_measure\_name: FK(Dose\_Measure)  
&emsp;&emsp;NOT NULL(dose\_measure\_name)  
&emsp;&emsp;NOT NULL(quantity)  
&emsp;&emsp;UNIQUE(quantity, dose\_measure\_name)  
&emsp;&emsp;IC-72  
&nbsp;  
Medicine(<u>medicine\_name</u>, active\_ingredient)  
&emsp;&emsp;IC-145  
&nbsp;  
Administration\_Route(<u>admin\_route\_name</u>)  
&emsp;&emsp;admin\_route\_name: ENUM  
&emsp;&emsp;IC-20  
&nbsp;  
medicine\_routes(<u>medicine\_name, admin\_route\_name</u>)  
&emsp;&emsp;medicine\_name: FK(Medicine)  
&emsp;&emsp;admin\_route\_name: FK(Administration\_Route)  
&emsp;&emsp;IC-149  
&nbsp;  
Prescription\_Period\_Unit(<u>presc\_period\_unit\_name</u>)  
&emsp;&emsp;presc\_period\_unit\_name: ENUM  
&emsp;&emsp;IC-19  
&nbsp;  
Day\_of\_Month(<u>day\_of\_month\_number</u>)  
&emsp;&emsp;IC-18, IC-56  
&nbsp;  
Moment\_of\_Day(<u>moment\_of\_day\_name</u>)  
&emsp;&emsp;moment\_of\_day\_name: ENUM  
&emsp;&emsp;IC-17  
&nbsp;  
Prescription\_Date(<u>presc\_date</u>)  
&nbsp;  
Prescription\_Schedule(<u>presc\_schedule\_number</u>)  
&emsp;&emsp;IC-146, IC-147  
&nbsp;  
SOS\_Prescription\_Schedule(<u>presc\_schedule\_number</u>, description)  
&emsp;&emsp;NOT NULL(description)  
&emsp;&emsp;IC-146, IC-147  
&nbsp;  
Recurrent\_Prescription\_Schedule(<u>presc\_schedule\_number</u>, start\_date, end\_date, frequency, period,&nbsp;presc\_period\_unit\_name)  
&emsp;&emsp;presc\_schedule\_number: FK(Prescription\_Schedule)  
&emsp;&emsp;presc\_period\_unit\_name: FK(Prescription\_Period\_Unit)  
&emsp;&emsp;IC-57, IC-58, IC-59, IC-90, IC-91, IC-92, IC-93, IC-94, IC-95, IC-96, IC-97, IC-146, IC-147  
&nbsp;  
Non\_Recurrent\_Prescription\_Schedule(<u>presc\_schedule\_number)</u>  
&emsp;&emsp;presc\_schedule\_number: FK(Prescription\_Schedule)  
&emsp;&emsp;IC-146, IC-147  
&nbsp;  
recurrent\_prescription\_schedule\_days\_of\_week(<u>presc\_schedule\_number, day\_of\_week\_name</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Recurrent\_Prescription\_Schedule)  
&emsp;&emsp;day\_of\_week\_name: FK(Day\_of\_Week)  
&nbsp;  
recurrent\_prescription\_schedule\_months(<u>presc\_schedule\_number,</u>&nbsp;<u>day\_of\_month\_number</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Recurrent\_Prescription\_Schedule)  
&emsp;&emsp;day\_of\_month\_number: FK(Day\_of\_Month)  
&nbsp;  
recurrent\_prescription\_schedule\_moment(<u>presc\_schedule\_number, moment\_of\_day\_name</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Recurrent\_Prescription\_Schedule)  
&emsp;&emsp;moment\_of\_day\_name: FK(Moment\_of\_Day)  
&nbsp;  
non\_recurrent\_prescription\_schedule\_simple\_dates(<u>presc\_schedule\_number, presc\_date</u>)  
&emsp;&emsp;presc\_schedule\_number: FK(Non\_Recurrent\_Prescription\_Schedule)  
&emsp;&emsp;presc\_date: FK(Prescription\_Date)  
&nbsp;  
non\_recurrent\_prescription\_schedule\_moment\_dates(<u>presc\_schedule\_number, presc\_date, moment\_of\_day\_name</u>)  
&emsp;&emsp;presc\_schedule\_number, presc\_date: FK(non\_recurrent\_prescription\_schedule\_simple\_dates)  
&emsp;&emsp;moment\_of\_day\_name: FK(Moment\_of\_Day)  
&nbsp;  
Prescription(<u>prescription\_number, client\_cc</u>, medicine\_name,&nbsp;dose\_id, admin\_route\_name, presc\_schedule\_number, cc\_who\_regists, regist\_date, cc\_who\_cancels, cancel\_date)  
&emsp;&emsp;client\_cc: FK(Client)  
&emsp;&emsp;medicine\_name: FK(Medicine)  
&emsp;&emsp;dose\_id: FK(Dose)  
&emsp;&emsp;admin\_route\_name: FK(Administration\_Route)  
&emsp;&emsp;presc\_schedule\_number: FK(Prescription\_Schedule)  
&emsp;&emsp;cc\_who\_regists: FK(Collaborator)  
&emsp;&emsp;cc\_who\_cancels: FK(Collaborator)  
&emsp;&emsp;NOT NULL(medicine\_name)  
&emsp;&emsp;NOT NULL(dose\_id)  
&emsp;&emsp;NOT NULL(admin\_route\_name)  
&emsp;&emsp;NOT NULL(presc\_schedule\_number)  
&emsp;&emsp;NOT NULL(cc\_who\_regists)  
&emsp;&emsp;NOT NULL(regist\_date)  
&emsp;&emsp;IC-88, IC-89, IC-143, IC-148  
&nbsp;  
Medicine\_Administration(<u>med\_admin\_date\_time, client\_cc, medicine\_name</u>, dose\_id, observations,&nbsp;coll\_cc, admin\_route\_name, prescription\_number)  
&emsp;&emsp;client\_cc: FK(Client)  
&emsp;&emsp;medicine\_name: FK(Medicine)  
&emsp;&emsp;dose\_id: FK(Dose)  
&emsp;&emsp;coll\_cc: FK(Collaborator)  
&emsp;&emsp;admin\_route\_name: FK(Administration\_Route)  
&emsp;&emsp;prescription\_number, client\_cc: FK(Prescription)  
&emsp;&emsp;NOT NULL(dose\_id)  
&emsp;&emsp;NOT NULL(coll\_cc)  
&emsp;&emsp;NOT NULL(admin\_route\_name)  
&emsp;&emsp;IC-84, IC-85, IC-86, IC-87, IC-144, IC-145  
&nbsp;  
&nbsp;  
**\#\# Observations and Occurrence**  
&nbsp;  
Patient\_Observation(<u>observation\_id</u>, patient\_cc, coll\_cc, created\_at, observed\_at, content)  
&emsp;&emsp;patient\_cc: FK(Patient)  
&emsp;&emsp;NOT NULL(patient\_cc)  
&emsp;&emsp;coll\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(coll\_cc)  
&emsp;&emsp;NOT NULL(created\_at)  
&emsp;&emsp;NOT NULL(observed\_at)  
&emsp;&emsp;NOT NULL(content)  
&emsp;&emsp;IC-138  
&nbsp;  
Occurrence\_Category(<u>occ\_category\_name</u>):  
&emsp;&emsp;occ\_category\_name: ENUM  
&emsp;&emsp;IC-21, IC-152  
&nbsp;  
Patient\_Occurrence\_Category(<u>occ\_category\_name</u>, is\_active)  
&emsp;&emsp;occ\_category\_name: FK(Occurrence\_Category)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-22, IC-152  
&nbsp;  
Child\_Occurrence\_Category(<u>occ\_category\_name</u>, is\_active)  
&emsp;&emsp;occ\_category\_name: FK(Occurrence\_Category)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-23, IC-152  
&nbsp;  
Occurrence(<u>occ\_number</u>,&nbsp;occ\_date\_time,&nbsp;description, coll\_cc)  
&emsp;&emsp;coll\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(occ\_date\_time)  
&emsp;&emsp;NOT NULL(coll\_cc)  
&emsp;&emsp;IC-150, IC-151  
&nbsp;  
Patient\_Occurrence(<u>occ\_number</u><u>,</u>&nbsp;<u>patient\_cc</u>, occ\_category\_name)  
&emsp;&emsp;occ\_number: FK(Occurrence)  
&emsp;&emsp;patient\_cc: FK(Patient)  
&emsp;&emsp;occ\_category\_name: FK(Patient\_Occurrence\_Category)  
&emsp;&emsp;NOT NULL(occ\_category\_name)  
&emsp;&emsp;UNIQUE(patient\_cc, occ\_date\_time, occ\_category\_name)  
&emsp;&emsp;IC-150, IC-151, IC-153  
&nbsp;  
Child\_Occurrence(<u>occ\_number</u><u>, child\_</u><u>cc</u>,&nbsp;occ\_category\_name)  
&emsp;&emsp;occ\_number: FK(Occurrence)  
&emsp;&emsp;child\_cc: FK(Child)  
&emsp;&emsp;occ\_category\_name: FK(Child\_Occurrence\_Category)  
&emsp;&emsp;NOT NULL(occ\_category\_name)  
&emsp;&emsp;UNIQUE(child\_cc, occ\_date\_time, occ\_category\_name)  
&emsp;&emsp;IC-150, IC-151, IC-163  
&nbsp;  
**\#\# Services, Tasks and Visits (Home Care Service and Senior Day Care)**  
&nbsp;  
Care\_Service\_Category(<u>care\_</u><u>service\_cat\_</u><u>name</u>)  
&emsp;&emsp;care\_service\_cat\_name: ENUM  
&emsp;&emsp;IC-24  
&nbsp;  
Care\_Service(<u>care\_</u><u>service\_name</u>, care\_service\_cat\_name)  
&emsp;&emsp;care\_service\_name: ENUM  
&emsp;&emsp;care\_service\_cat\_name: FK(Care\_Service\_Category)  
&emsp;&emsp;IC-25, IC-158  
&nbsp;  
Home\_Care\_Service(<u>care\_service\_name</u>, is\_active)  
&emsp;&emsp;care\_service\_name: FK(Care Service)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-26, IC-158  
&nbsp;  
Day\_Care\_Service(<u>care\_service\_name</u>, is\_active)  
&emsp;&emsp;care\_service\_name: FK(Care Service)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-27, IC-158  
&nbsp;  
Biometric\_Service(<u>care\_service\_name</u>, biometric\_unit, primary\_label, secondary\_label)  
&emsp;&emsp;care\_service\_name: FK(Care\_Service)  
&emsp;&emsp;NOT NULL(biometric\_unit)  
&emsp;&emsp;NOT NULL(primary\_label)  
&emsp;&emsp;IC-158, IC-196  
&nbsp;  
home\_care\_patient\_service\_list(<u>patient\_cc</u><u>, care\_</u><u>service\_name</u><u>,</u>&nbsp;<u>day\_of\_week\_name, valid\_since, valid\_until</u>)  
&emsp;&emsp;patient\_cc: FK(Home\_Care\_Patient)  
&emsp;&emsp;care\_service\_name: FK(Home\_Care\_Service)  
&emsp;&emsp;day\_of\_week\_name: FK(Day\_of\_Week)  
&emsp;&emsp;valid\_since, valid\_until: FK(Validation\_Period)  
&emsp;&emsp;IC-73, IC-85  
&nbsp;  
day\_care\_patient\_service\_list(<u>patient\_cc</u><u>, care\_</u><u>service\_name</u><u>,</u>&nbsp;<u>day\_of\_week\_name, valid\_since, valid\_until</u>)  
&emsp;&emsp;patient\_cc: FK(Day\_Care\_Patient)  
&emsp;&emsp;care\_service\_name: FK(Day\_Care\_Service)  
&emsp;&emsp;day\_of\_week\_name: FK(Day\_of\_Week)  
&emsp;&emsp;valid\_since, valid\_until: FK(Validation\_Period)  
&emsp;&emsp;IC-73, IC-84  
&nbsp;  
Visit(<u>visit\_date, arrival\_time,</u>&nbsp;<u>patient\_cc</u>, departure\_time, patient\_signature\_path, observations)  
&emsp;&emsp;patient\_cc: FK(Home\_Care\_Patient)  
&emsp;&emsp;NOT NULL(departure\_time)  
&emsp;&emsp;NOT NULL(patient\_signature\_path)  
&emsp;&emsp;IC-60, IC-155  
&nbsp;  
visit\_services(<u>visit\_date, arrival\_time</u><u>,</u>&nbsp;<u>patient\_cc</u><u>, care\_</u><u>service\_name</u>)  
&emsp;&emsp;visit\_date, arrival\_time,&nbsp;patient\_cc: FK(Visit)  
&emsp;&emsp;care\_service\_name: FK(Home\_Care\_Service)  
&nbsp;  
visit\_collaborators(<u>visit\_date, arrival\_time</u><u>, patient\_cc, coll\_cc</u>)  
&emsp;&emsp;visit\_date, arrival\_time, patient\_cc: FK(Visit)  
&emsp;&emsp;coll\_cc: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;IC-156  
&nbsp;  
Care\_Task(<u>patient\_cc, task\_timestamp, care\_service\_name</u>, observations, coll\_cc)  
&emsp;&emsp;patient\_cc: FK(Day\_Care\_Patient)  
&emsp;&emsp;coll\_cc: FK(Day\_Care\_Collaborator)  
&emsp;&emsp;care\_service\_name: FK(Day\_Care\_Service)  
&emsp;&emsp;NOT NULL(coll\_cc)  
&emsp;&emsp;IC-154, IC-157  
&nbsp;  
Biometric\_Task(<u>patient\_cc, task\_timestamp, care\_service\_name</u>, biometric\_value, biometric\_value\_secondary)  
&emsp;&emsp;patient\_cc, task\_timestamp, care\_service\_name: FK(Care\_Task)  
&emsp;&emsp;NOT NULL(biometric\_value)  
&emsp;&emsp;IC-157, IC-194, IC-195  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Zones, Shifts and Requests (Home Care Service Specific)**  
&nbsp;  
Zone(<u>zone\_name</u>, min\_collab, is\_active)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-28  
&nbsp;  
Zone\_Hours(<u>start\_time, start\_break\_time, end\_break\_time, end\_time</u>)  
&emsp;&emsp;IC-29, IC-62
  
Holiday(<u>holiday\_date</u>, holiday\_name, is\_working\_holiday)  
&emsp;&emsp;NOT NULL(holiday\_name)  
&emsp;&emsp;NOT NULL(is\_working\_holiday)  
&nbsp;  
zone\_schedule\_hours(<u>zone\_name, start\_time, start\_break\_time, end\_break\_time, end\_time, valid\_since, valid\_until</u>)  
&emsp;&emsp;zone\_name: FK(Zone)  
&emsp;&emsp;start\_time, start\_break\_time, end\_break\_time, end\_time: FK(Zone\_Hours)  
&emsp;&emsp;valid\_since, valid\_until: FK(Validation\_Period)  
&emsp;&emsp;IC-31, IC-73, IC-160  
&nbsp;  
zone\_schedule\_week(<u>zone\_name, day\_of\_week\_name, valid\_since, valid\_until</u>)  
&emsp;&emsp;zone\_name: FK(Zone)  
&emsp;&emsp;day\_of\_week\_name: FK(Day\_of\_Week)  
&emsp;&emsp;valid\_since, valid\_until: FK(Validation\_Period)  
&emsp;&emsp;IC-30, IC-73  
&nbsp;  
holiday\_zone\_availability(<u>holiday\_date, zone\_name</u>)  
&emsp;&emsp;holiday\_date: FK(Holiday)  
&emsp;&emsp;zone\_name: FK(Zone)  
&emsp;&emsp;IC-100  
&nbsp;  
zone\_patient\_list(<u>zone\_name, cc, valid\_since</u><u>, valid\_unti</u>l,&nbsp;visit\_order)  
&emsp;&emsp;zone\_name: FK(Zone)  
&emsp;&emsp;cc: FK(Home\_Care\_Patient)  
&emsp;&emsp;valid\_since, valid\_until: FK(Validation\_Period)  
&emsp;&emsp;IC-61, IC-73, IC-98  
&nbsp;  
Shift\_Schedule\_Period(<u>start\_date, end\_date</u>, is\_published, admin\_cc)  
&emsp;&emsp;admin\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(is\_published)  
&emsp;&emsp;NOT NULL(admin\_cc)  
&emsp;&emsp;IC-59,&nbsp;IC-101  
&nbsp;  
Schedule\_Job(<u>start\_date, end\_date, job\_number</u>,&nbsp;admin\_cc, requested\_date\_time, status, error\_message)  
&emsp;&emsp;start\_date, end\_date: FK(Shift\_Schedule\_Period)  
&emsp;&emsp;admin\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(admin\_cc)  
&emsp;&emsp;NOT NULL(requested\_date\_time)  
&emsp;&emsp;NOT NULL(status)  
&emsp;&emsp;IC-64  
&nbsp;  
Shift(<u>zone\_name, date</u>, start\_date, end\_date)  
&emsp;&emsp;zone\_name: FK(Zone)  
&emsp;&emsp;start\_date, end\_date: FK(Shift\_Schedule\_Period)  
&emsp;&emsp;NOT NULL(start\_date)  
&emsp;&emsp;NOT NULL(end\_date)  
&emsp;&emsp;IC-102  
&nbsp;  
shift\_assignment(<u>zone\_name, date,</u>&nbsp;<u>coll\_cc</u>)  
&emsp;&emsp;zone\_name, date: FK(Shift)  
&emsp;&emsp;coll\_cc: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;IC-99, IC-103, IC-104, IC-105, IC-106  
&nbsp;  
Request(<u>request\_number, coll\_cc</u>, date\_time, is\_expired)  
&emsp;&emsp;coll\_cc: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;NOT NULL(is\_expired)  
&emsp;&emsp;IC-159, IC-161, IC-162  
&nbsp;  
admin\_request\_evaluation(<u>request\_number, coll\_cc</u>,&nbsp;admin\_cc, is\_approved, approval\_date\_time)  
&emsp;&emsp;coll\_cc, request\_number: FK(Request)  
&emsp;&emsp;admin\_cc: FK(Collaborator)  
&nbsp;  
Absence(<u>request\_number, coll\_cc</u>, start\_date, end\_date, justification\_text)  
&emsp;&emsp;request\_number, coll\_cc: FK(Request)  
&emsp;&emsp;NOT NULL(start\_date)  
&emsp;&emsp;NOT NULL(end\_date)  
&emsp;&emsp;NOT NULL(justification\_text)  
&emsp;&emsp;IC-161, IC-162  
&nbsp;  
Vacation(<u>request\_number, coll\_cc</u>, start\_date, end\_date, comment\_text)  
&emsp;&emsp;coll\_cc, request\_number: FK(Request)  
&emsp;&emsp;NOT NULL(start\_date)  
&emsp;&emsp;NOT NULL(end\_date)  
&emsp;&emsp;IC-59, IC-161, IC-162  
&nbsp;  
Time\_Off\_Swap(<u>request\_number, coll\_cc</u>, original\_date, requested\_date, comment\_text)  
&emsp;&emsp;request\_number, coll\_cc: FK(Request)  
&emsp;&emsp;NOT NULL(original\_date)  
&emsp;&emsp;NOT NULL(requested\_date)  
&emsp;&emsp;IC-63  
&nbsp;  
Shift\_Swap(<u>request\_number, coll\_cc</u>, from\_zone, from\_date, to\_zone, to\_date,&nbsp;to\_cc, comment\_text)  
&emsp;&emsp;request\_number, coll\_cc: FK(Request)  
&emsp;&emsp;to\_cc: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;from\_zone, from\_date,&nbsp;coll\_cc: FK(shift\_assignment)  
&emsp;&emsp;to\_zone, to\_date,&nbsp;to\_cc: FK(shift\_assignment)  
&emsp;&emsp;NOT NULL(from\_zone)  
&emsp;&emsp;NOT NULL(from\_date)  
&emsp;&emsp;IC-107, IC-108, IC-109, IC-110, IC-161, IC-162  
&nbsp;  
home\_care\_collaborator\_swap\_acceptance(<u>request\_number,</u>&nbsp;<u>from\_</u><u>cc,</u>&nbsp;<u>to\_</u><u>cc,</u>&nbsp;is\_accepted, acceptance\_date\_time)  
&emsp;&emsp;request\_number,&nbsp;from\_cc: FK(Shift\_Swap)  
&emsp;&emsp;to\_cc: FK(Home\_Care\_Collaborator)  
&emsp;&emsp;IC-65  
&nbsp;  
&nbsp;  
&nbsp;  
**\#\# Child Specifics**  
&nbsp;  
Feeding(<u>child\_cc, date\_time</u>, is\_lunch, observations,&nbsp;auxiliar\_cc)  
&emsp;&emsp;<u>child\_cc</u>: FK(Child)  
&emsp;&emsp;auxiliar\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(is\_lunch)  
&emsp;&emsp;NOT NULL(auxiliar\_cc)  
&emsp;&emsp;IC-164  
&nbsp;  
Hygiene(<u>child\_cc, date\_time</u>,&nbsp;auxiliar\_cc, hygiene\_type)  
&emsp;&emsp;child\_cc: FK(Child)  
&emsp;&emsp;type: enum  
&emsp;&emsp;auxiliar\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(auxiliar\_cc)  
&emsp;&emsp;NOT NULL (type)  
&emsp;&emsp;IC-33, IC-165  
&nbsp;  
Attendance(<u>child\_cc, date\_time</u>,&nbsp;auxiliar\_cc,&nbsp;companion\_cc, is\_entry)  
&emsp;&emsp;child\_cc: FK(Child)  
&emsp;&emsp;auxiliar\_cc: FK(Collaborator)  
&emsp;&emsp;companion\_cc: FK(Person)  
&emsp;&emsp;NOT NULL(auxiliar\_cc)  
&emsp;&emsp;NOT NULL(is\_entry)  
&emsp;&emsp;IC-66,&nbsp;IC-166, IC-185, IC-186  
&nbsp;  
&nbsp;  
Activity\_Session(<u>date,</u>&nbsp;<u>is\_in\_the\_m</u><u>orning</u><u>, name</u>,&nbsp;description,&nbsp;auxiliar\_cc)  
&emsp;&emsp;auxiliar\_cc: FK(Collaborator)  
&emsp;&emsp;name: FK(Activity)  
&emsp;&emsp;NOT NULL(auxiliar\_cc)  
&nbsp;  
Activity(<u>name</u>)  
&nbsp;  
child\_activity(<u>child\_cc, date, is\_in\_the\_morning, name,</u>&nbsp;individual\_notes)  
&emsp;&emsp;child\_cc: FK(Child)  
&emsp;&emsp;date, is\_in\_the\_morning, name: FK(Activity\_Session)  
&nbsp;  
Photo(<u>file\_path, upload\_time</u>, caption,&nbsp;auxiliar\_cc, date, is\_in\_the\_morning,&nbsp;name)  
&emsp;&emsp;auxiliar\_cc: FK(Collaborator)  
&emsp;&emsp;date, is\_in\_the\_morning,&nbsp;name&nbsp;: FK(Activity\_Session)  
&emsp;&emsp;NOT NULL(auxiliar\_cc)  
&emsp;&emsp;IC-111, IC-116  
&nbsp;  
child\_photo(<u>child\_cc, filepath, upload\_time</u>)  
&emsp;&emsp;child\_cc: FK(Child)  
&emsp;&emsp;filepath, upload\_time: FK(Photo)  
&emsp;&emsp;IC-115  
&nbsp;  
Authorization\_Form<u>(child\_cc, valid\_since, authorized\_person\_cc</u>, guardian\_cc,&nbsp;educator\_cc,  valid\_until, status, relationship)  
&emsp;&emsp;child\_cc: FK(Child)  
&emsp;&emsp;authorized\_person\_cc: FK(Person)  
&emsp;&emsp;guardian\_cc: FK(Guardian)  
&emsp;&emsp;educator\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(guardian\_cc)  
&emsp;&emsp;NOT NULL(start\_date)  
&emsp;&emsp;NOT NULL(end\_date)  
&emsp;&emsp;NOT NULL(status)  
&emsp;&emsp;NOT NULL (relationship)  
&emsp;&emsp;IC-34, IC-49, IC-73, IC-117, IC-169, IC-188  
&nbsp;  
Pedagogical\_Evaluation(<u>child\_cc, date\_time</u>, educator\_cc)  
&emsp;&emsp;educator\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(educator\_cc)  
&emsp;&emsp;IC-167
  
&nbsp;  
&emsp;&emsp;Evaluation\_Theme&nbsp;&nbsp;(<u>child\_cc, date\_time, category\_name</u>, objectives, actions, resources,&nbsp;assessment)  
&emsp;&emsp;child\_cc, date\_time: FK(Pedagogical\_Evaluation)  
&emsp;&emsp;category\_name: FK(Evaluation\_Category)  
&nbsp;  
Individual\_Educational\_Plan(<u>child\_cc, date\_time</u>, educator\_cc)  
&emsp;&emsp;child\_cc: FK(Child)  
&emsp;&emsp;educator\_cc: FK(Collaborator)  
&emsp;&emsp;NOT NULL(educator\_cc)  
&emsp;&emsp;IC-16, IC-189  
&nbsp;  
Evaluation\_Category(<u>category\_name</u>,  is\_active)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-38,&nbsp;IC-112, IC-172  
&nbsp;  
Evaluation\_Subcategory(<u>subcategory\_name, category\_name,</u>&nbsp;is\_active)  
&emsp;&emsp;subcategory\_name: ENUM  
&emsp;&emsp;category\_name: FK(Evaluation\_Category)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;IC-39, IC-40, IC-113, IC-171  
&nbsp;  
&nbsp;  
Milestone(<u>milestone\_name , subcategory\_name, category\_name, group\_name</u>, is\_active)  
&emsp;&emsp;subcategory\_name, category\_name: FK(Evaluation\_Subcategory)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;group\_name: FK(age\_group)  
&emsp;&emsp;IC-41, IC-42  
&nbsp;  
&nbsp;  
Measure\_Label(<u>measure\_label\_name</u>)  
&emsp;&emsp;measure\_label\_name: ENUM  
&emsp;&emsp;IC-35  
&nbsp;  
plan\_milestone\_status(<u>child\_cc, plan\_date\_time, milestone\_name, subcategory\_name, category\_name, group\_name</u>,&nbsp;measure\_label\_name)  
&emsp;&emsp;child\_cc, plan\_date\_time: FK(Individual\_Educational\_Plan)  
&emsp;&emsp;milestone\_name, subcategory\_name, category\_name,&nbsp;group\_name: FK(Milestone)  
&emsp;&emsp;measure\_label\_name: FK(Measure\_Label)  
&emsp;&emsp;NOT NULL(measure\_label\_name)  
&emsp;&emsp;IC-114  
&nbsp;  
&nbsp;  
**\#\# Assets**  
&nbsp;  
Supplier(<u>n</u><u>if</u>, name, fiscal\_address, supply\_address, business\_sector, contact\_person\_name, mobile\_phone, landline\_phone, primary\_email, secondary\_email, supplier\_created\_date, bank\_name, iban, swift\_code, internal\_supplier\_rating, important\_notes, general\_notes)  
&emsp;&emsp;NOT NULL(name)  
&emsp;&emsp;NOT NULL(fiscal\_address)  
&emsp;&emsp;NOT NULL(supply\_address)  
&emsp;&emsp;NOT NULL(business\_sector)  
&emsp;&emsp;NOT NULL(contact\_person\_name)  
&emsp;&emsp;NOT NULL(mobile\_phone)  
&emsp;&emsp;NOT NULL(landline\_phone)  
&emsp;&emsp;NOT NULL(primary\_email)  
&emsp;&emsp;NOT NULL(secondary\_email)  
&emsp;&emsp;NOT NULL(supplier\_created\_date)  
&emsp;&emsp;NOT NULL(bank\_name)  
&emsp;&emsp;NOT NULL(iban)  
&emsp;&emsp;NOT NULL(swift\_code)  
&emsp;&emsp;NOT NULL(internal\_supplier\_rating)  
&emsp;&emsp;important\_notes  
&emsp;&emsp;general\_notes  
&nbsp;  
Asset\_Location(<u>location\_name</u>)  
&emsp;&emsp;location\_name: ENUM  
&emsp;&emsp;IC-43
  
Asset\_Category(<u>category\_name</u>)  
&emsp;&emsp;category\_name: ENUM  
&emsp;&emsp;IC-46
  
Asset(<u>asset\_code</u>, is\_active, disposal\_date, location, technical\_characteristics, acquisition\_date, service\_start\_date, acquisition\_cost, designation, supplier, category\_name)  
&emsp;&emsp;NOT NULL(is\_active)  
&emsp;&emsp;disposal\_date  
&emsp;&emsp;NOT NULL(location)  
&emsp;&emsp;NOT NULL(technical\_characteristics)  
&emsp;&emsp;NOT NULL(acquisition\_date)  
&emsp;&emsp;service\_start\_date  
&emsp;&emsp;NOT NULL(acquisition\_cost)  
&emsp;&emsp;NOT NULL(designation)  
&emsp;&emsp;supplier: FK(Supplier)  
&emsp;&emsp;NOT NULL(supplier)  
&emsp;&emsp;category\_name: FK(Asset\_Category)  
&emsp;&emsp;NOT NULL(category\_name)  
&emsp;&emsp;IC-43, IC-120, IC-121, IC-175, IC-176, IC-177, IC-195  
&nbsp;  
&nbsp;  
Intervention\_Status(<u>status\_name</u>)  
&emsp;&emsp;status\_name: ENUM  
&emsp;&emsp;IC-44  
&nbsp;  
Intervention\_Category(<u>category\_name</u>)  
&emsp;&emsp;category\_name: ENUM  
&emsp;&emsp;IC-45  
&nbsp;  
Expense\_Type<u>(expense\_type\_name</u>)  
&emsp;&emsp;expense\_type\_name: ENUM  
&emsp;&emsp;IC-47  
&nbsp;  
Intervention(<u>asset\_code, intervention\_date</u>, description, status\_name, category\_name, cc\_who\_regists)  
&emsp;&emsp;asset\_code: FK(Asset)  
&emsp;&emsp;NOT NULL(description)  
&emsp;&emsp;status\_name: FK(Intervention\_Status)  
&emsp;&emsp;category\_name: FK(Intervention\_Category)  
&emsp;&emsp;NOT NULL(category\_name)  
&emsp;&emsp;NOT NULL(status\_name)  
&emsp;&emsp;cc\_who\_regists: FK(Collaborator)  
&emsp;&emsp;IC-122, IC-126, IC-127, IC-128, IC-129, IC-132, IC-173, IC-174, IC-175, IC-322  
&nbsp;  
&nbsp;  
Email(<u>asset\_code, date\_time</u>, subject, storage\_path, cc\_who\_upload)  
&emsp;&emsp;asset\_code: FK(Asset)  
&emsp;&emsp;NOT NULL(subject),  
&emsp;&emsp;NOT NULL(storage\_path)  
&emsp;&emsp;cc\_who\_upload: FK(Collaborator)  
&emsp;&emsp;IC-67, IC-118, IC-176, IC-178, IC-180, IC-182, IC-321  
&nbsp;  
&nbsp;  
Document(<u>asset\_code, filename,</u>&nbsp;date, file\_path)  
&emsp;&emsp;asset\_code: FK(Asset)  
&emsp;&emsp;NOT NULL(date),  
&nbsp;  
&emsp;&emsp;NOT NULL(file\_path)  
&emsp;&emsp;IC-68, IC-125, IC-130, IC-177, IC-179, IC-181, IC-182  
&nbsp;  
&nbsp;  
Normal\_Document(<u>asset\_code, filename</u>)  
&nbsp;  
&emsp;&emsp;asset\_code, filename: FK(Document)  
&nbsp;  
&nbsp;  
Expense\_Document(<u>asset\_code, filename,</u>&nbsp;expense\_asset\_code, intervention\_date, expense\_date)  
&nbsp;  
&emsp;&emsp;asset\_code, filename: FK(Document)  
&nbsp;  
&emsp;&emsp;expense\_asset \_code, intervention\_date, expense\_date: FK(Expense)  
&nbsp;  
&nbsp;  
&nbsp;  
Intervention\_Document(<u>asset\_code, filename,</u>&nbsp;intervention\_asset\_code, intervention\_date)  
&nbsp;  
&emsp;&emsp;asset\_code, filename: FK(Document)  
&nbsp;  
&emsp;&emsp;intervention\_asset \_code, intervention\_date: FK(Intervention)  
&nbsp;  
email\_document(<u>email\_asset\_code, date\_time, document\_asset\_code, filename</u>)  
&emsp;&emsp;email\_asset\_code, date\_time: FK(Email)  
&emsp;&emsp;document\_asset\_code, filename: FK(Document)  
&emsp;&emsp;IC-114, IC-178, IC-179, IC-180, IC-181, IC-182  
&nbsp;  
Expense(<u>asset\_code, intervention\_date, date</u>, description, associated\_cost, expense\_type\_name)  
&emsp;&emsp;asset\_code, intervention\_date: FK(Intervention)  
&emsp;&emsp;NOT NULL(description),  
&emsp;&emsp;NOT NULL(description)  
&emsp;&emsp;expense\_type\_name: FK(Expense\_Type)  
&emsp;&emsp;NOT NULL(expense\_type\_name)  
&emsp;&emsp;IC-124, IC-173, IC-196, IC-456  
&nbsp;  
Alert(<u>asset\_code, intervention\_date, alert\_date</u>, advance\_notification\_period)  
&emsp;&emsp;asset\_code, intervention\_date: FK(Intervention)  
&emsp;&emsp;NOT NULL(advance\_notification\_period)  
&emsp;&emsp;IC-119, IC-123, IC-131, IC-174, IC-197  
