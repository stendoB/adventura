__pycache__/                                                                                        0000775 0001750 0001750 00000000000 14120125706 012714  5                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 __pycache__/states.cpython-38.pyc                                                                   0000664 0001750 0001750 00000000275 14120125636 016655  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 U
    m?@a   ?                   @   s   d Z dZdZdS )?    ?   ?   N)ZQUIT?PLAYING?WIN? r   r   ?2/home/ubuntu/git/docker_images/adventura/states.py?<module>   s                                                                                                                                                                                                                                                                                                                                      __pycache__/helper.cpython-38.pyc                                                                   0000664 0001750 0001750 00000001027 14120125706 016623  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 U
    J?@a)  ?                   @   s(   e eed ?dd?Ze eed?dd?ZdS ))?name?items?returnc                 C   s"   |D ]}|d | kr|  S qd S ?Nr   ? )r   r   ?itemr   r   ?2/home/ubuntu/git/docker_images/adventura/helper.py?	find_item   s    
r   )r   ?worldr   c                 C   s"   |D ]}|d | kr|  S qd S r   r   )r   r	   ?roomr   r   r   ?get_room_by_name	   s    
r   N)?str?list?dictr   r   r   r   r   r   ?<module>   s                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            __pycache__/commands.cpython-38.pyc                                                                 0000664 0001750 0001750 00000014345 14120125706 017154  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 U
    #?@a?#  ?                   @   s?  d dl Z d dlZd dlZd dlZd dlmZmZ eedd?dd?Z	eedd?dd?Z
eedd?dd	?Zeedd?d
d?Zeedd?dd?Zeedd?dd?Zeedd?dd?Zeedd?dd?Zeedd?dd?Zeedd?dd?Zeedd?dd?Zeedd?dd?Zeedd?dd?Zdded d!?d"d#ed$d!?d%d&d'ed(?d)d*d+ed(?d,d-d.e
d(?d/d0d1e	d(?d2d3d4ed(?d5d6d7dd(?d8d9d:ed(?d;d<d=ed(?d>d?d@ed(?dAdBdCed(?dDdEdFed(?gZdS )G?    N)?	find_item?get_room_by_name)?name?context?returnc                 C   sF   t |d ?dkrtd? n(td? |d D ]}td|d ? ?? q*d S )N?	inventoryr   u   Batoh je prázdny.u   V batohu máš:?	* r   ??len?print?r   r   ?item? r   ?4/home/ubuntu/git/docker_images/adventura/commands.pyr   	   s
    
r   c                 C   s?   |d }t d|d ? d?? t |d ? ? t|d ?dkrDt d? n(t d	? |d D ]}t d
|d ? ?? qTddddd?}t d? |d D ]&}|d | d k	r?t d
|| ? ?? q?d S )N?roomu   Nachádzaš sa v miestnosti r   ?.?description?itemsr   u   Nevidíš tu nič zaujímavé.u   Vidíš:r   ?sever?juh?vychod?zapad)?north?south?east?westu   Východy z miestnosti:?exits)r   r
   )r   r   r   r   ZtranslationZexr   r   r   ?look_around   s"    
?r   c                 C   sl   | dkrt d? nV|d D ]D}|d | kr|d ?|? |d d ?|? t d| ? d??  qhqt d	? d S )
N? u&   Neviem, aký predmet chceš položiť.r   r   r   r   ?Predmet u    si vyložil do miestnosti.u   Taký predmet u seba nemáš.)r   ?remove?appendr   r   r   r   ?drop,   s    
r"   c                 C   s?   |d }|d }| dkr"t d? n||d D ]j}|d | kr*t|?dkrPt d? n@tj|d	 kr?|d ?|? |?|? t d
| ? d?? nt d?  q?q*t d? dS )z?
    Represents the TAKE command.
    :param name: the name of item do describe
    :param room: the room object, where the player is currently in
    :param inventory: the player's inventory
    r   r   r   u#   Neviem, aký predmet chceš vziať.r   r   ?   u   Batoh je plný.?featuresr   u    si si vložil do batohu.u   Tento predmet sa nedá zobrať.?    Taký predmet tu nikde nevidím.N)r   r
   r$   ?MOVABLEr    r!   ?r   r   r   r   r   r   r   r   ?take>   s    


r(   c                 C   s`   |d }|d }t | ?dkr&td? n6|d | D ] }|d | kr2t|d ?  q\q2td? d	S )
z?
    Represents the examine command.
    :param name: the name of item do describe
    :param room: the room object, where the player is currently in
    :param inventory: the player's inventory
    r   r   r   u(   Neviem, aký predmet chceš preskúmať.r   r   r   u    Taký predmet tu nigde nevidím.Nr	   r'   r   r   r   ?examined   s    
r)   c                 C   s?   |d }|d }t | ?dkr(td? dS t| |d | ?}|dkrNtd? dS tj|d krhtd	? dS | d
kr~t?||? nP| dkr?t?||? n:| dkr?t?||? n$| dkr?t?	||? ntd| ? ?? dS )z|
    Represents the examine command.
    :param name: the name of item do describe
    :param context: the game context
    r   r   r   u%   Neviem, aký predmet chceš použiť.Nr   r%   r$   u    Tento predmet sa nedá použiť.zucebnica jazyka pythonZkanisterZzapalkyzhasiaci pristroju   Snažím sa použiť predmet )
r
   r   r   r$   ?USABLE?usagesZuse_textbookZuse_canZuse_matchesZuse_fire_extinguisherr'   r   r   r   ?usez   s*    r,   c                 C   s   t d? t d? d S )Nu   Hru spáchal v (c) 2021 mirek.uo   Ďalšie dobrodužstvo Indiana Jonesa. Tentokrát sa pokúsi o únik zo skladu Košického Technického múzea.?r   ?r   r   r   r   r   ?about?   s    r/   c                 C   s   t d? tj|d< d S )Nz
ta koncime?state)r   ?states?QUITr.   r   r   r   ?	quit_game?   s    r3   c                 C   s6   t d? |d D ] }t d|d ? d|d ? ?? qd S )Nu   Zoznam príkazov hry:?commandsr   r   z - r   r-   )r   r   ?commandr   r   r   ?show_commands?   s    r6   c                 C   sT   |d }|d d d kr$t d? d S |d d }t||d ?}||d< td |? d S )Nr   r   r   ?   Tam sa nedá ísť.?world?r   r   r   ?r   r   r   Z	room_nameZtarget_roomr   r   r   r   ?   s    r   c                 C   sT   |d }|d d d kr$t d? d S |d d }t||d ?}||d< td |? d S )Nr   r   r   r7   r8   r9   r:   r   r   r   r   ?   s    r   c                 C   sT   |d }|d d d kr$t d? d S |d d }t||d ?}||d< td |? d S )Nr   r   r   r7   r8   r9   r:   r   r   r   r   ?   s    r   c                 C   sT   |d }|d d d kr$t d? d S |d d }t||d ?}||d< td |? d S )Nr   r   r   r7   r8   r9   r:   r   r   r   r   ?   s    r   Z	preskumaj)r)   u(   zobrazí informácie o zvolenom predmete)r   ?aliases?execr   Zpoloz)r"   u4   vyberie predmet z batohu a položí ho do miestnostiZkoniec)?quitZbye?qZukoncitu   ukončí rozohratú hru)r   r;   r   r<   zo hre)r/   u   zobrazí informácie o hrezrozhliadni sa)zlook aroundu   zobrazí obsah miestnostiZinventar)r   ?iu   zobrazí obsah batohuZvezmi)r(   u1   vezme predmet z miestnosti a vloží ho do batohuZprikazy)r4   ?helpZpomocu+   zobrazí zoznam príkazov dostupných v hreZpouzi)Zpouzitr,   u   použije zvolený predmetr   )r   ?w?zzprejde do miestnosti na zapadr   )r   ?e?vzprejde do miestnosti na vychodr   )r   ?n?szprejde do miestnosti na severr   )r   ?jzprejde do miestnosti na juh)Zrandomr$   r1   r+   ?helperr   r   ?str?dictr   r   r"   r(   r)   r,   r/   r3   r6   r   r   r   r   r4   r   r   r   r   ?<module>   s?   	&+??????????????                                                                                                                                                                                                                                                                                           __pycache__/usages.cpython-38.pyc                                                                   0000664 0001750 0001750 00000006534 14120125706 016643  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 U
    ??@a-  ?                   @   s@   d dl Z d dlZd dlmZ dd? Zdd? Zdd? Zd	d
? ZdS )?    N)?	find_itemc                 C   sD   ddddddddd	d
dddddddddg}t d? t t?|?? d S )NzBeautiful is better than ugly.z!Explicit is better than implicit.zSimple is better than complex.z#Complex is better than complicated.zFlat is better than nested.zSparse is better than dense.zReadability counts.z7Special cases aren't special enough to break the rules.z#Although practicality beats purity.z"Errors should never pass silently.zUnless explicitly silenced.z9In the face of ambiguity, refuse the temptation to guess.zEThere should be one-- and preferably only one --obvious way to do it.zBAlthough that way may not be obvious at first unless you're Dutch.zNow is better than never.z0Although never is often better than *right* now.z:If the implementation is hard to explain, it's a bad idea.z@If the implementation is easy to explain, it may be a good idea.z@Namespaces are one honking great idea -- let's do more of those!u1   Zalistoval si v učebnici a dočítal si sa, že:)?print?random?choice)?item?contextZ_zen_of_python? r   ?2/home/ubuntu/git/docker_images/adventura/usages.py?use_textbook   s,    ?r
   c                 C   sh   |d }d| d< | d ? tj? td|d ?}|d k	r\|d dkr\d	|d< d
|d< td? ntd? d S )N?roomuE   Prázdny kanister. Po pričuchnutí je ti to jasné - bol tu benzín.?description?features?dvere?items?stateZzamknute?poliateu]   Dvere. Stále zamknuté, ale ako bonus sú poliate benzínom. Je ti jasné, kto za to môže.u?   Ta som odšroboval, rozohnal som sa a celý obsah kanistra som vylial na dvere. V miestnosti sa náhle rozľahol benzínový zápach. Proste vysoko-oktánová fajnotka.u;   Zahrkal som kanistrom a uistil som sa, že je stále plný.)?remover   ?USABLEr   r   ?r   r   r   ?doorr   r   r	   ?use_can"   s    
r   c                 C   s?   |d }|d }t d|d ?}|rv|d dkrv| |d krJ|d ?| ? n
|?| ? d|d< d|d	< d
|d< td? ntd? d S )Nr   ?	inventoryr   r   r   r   Zhoriaceue   Doteraz tie dvere iba voňali, teraz už aj horia. Zaujímavé, čo všetko sa dnes deje v tom svete.r   ?horiace dvere?nameu?   Zahrkal si krabičkou zápaliek a jednu si z nej vytiahol. Nadýchol si sa, škrtol si a ona chytila. Usmial si sa a s úsmevom na tvári si horiacu zápalku voľne pohodil smerom k dverám. Tie neváhali a okamžite zbĺkli. Ten benzín urobil svoje.uI   Krabička zápaliek. Nič zaujímavé. Len na čo by som ich tak použil?)r   r   r   )r   r   r   r   r   r   r   r	   ?use_matches8   s    
?r   c                 C   sb   |d }t d|d ?}|rV|d ?|? | d ?tj? d| d< d|d d	< td
? ntd? d S )Nr   r   r   r   u8   Ručný hasiaci prístroj prázdny. Značka - červený.r   ?garden?exits?westuc   Zahasil si dvere. Tie sa vplyvom tlaku hasiacej zmesy rozpadli a uvoľnili ti východ z miestnosti.u'   Aj by som nasnežil, ale nie je na čo.)r   r   r   r   r   r   r   r   r	   ?use_fire_extinguisherW   s    ?r   )r   r   ?helperr   r
   r   r   r   r   r   r   r	   ?<module>   s                                                                                                                                                                       __pycache__/features.cpython-38.pyc                                                                 0000664 0001750 0001750 00000000261 14120125636 017163  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 U
    7?@a   ?                   @   s   d Z dZdS )?   ?   N)?MOVABLE?USABLE? r   r   ?4/home/ubuntu/git/docker_images/adventura/features.py?<module>   s                                                                                                                                                                                                                                                                                                                                                  commands.py                                                                                         0000664 0001750 0001750 00000021710 14120125443 012656  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 import random

import features
import states
import usages
from helper import find_item, get_room_by_name


def inventory(name: str, context: dict) -> None:
    if len(context['inventory']) == 0:
        print('Batoh je prázdny.')
    else:
        print('V batohu máš:')
        for item in context['inventory']:
            print(f'\t* {item["name"]}')


def look_around(name: str, context: dict) -> None:
    room = context['room']
    print(f'Nachádzaš sa v miestnosti {room["name"]}.')
    print(f'{room["description"]}')

    if len(room['items']) == 0:
        print('Nevidíš tu nič zaujímavé.')
    else:
        print(f'Vidíš:')
        for item in room['items']:
            print(f'\t* {item["name"]}')

    # tuto vypisat vychody z miestnosti
    # alebo: Z miestnosti nevedú žiadne východy. v pripade, ze ziadne vychody nie su
    translation = {
        'north': 'sever',
        'south': 'juh',
        'east': 'vychod',
        'west': 'zapad'
    }
    print('Východy z miestnosti:')
    for ex in room['exits']:
        if room['exits'][ex] is not None:
            print(f'\t* {translation[ex]}')


def drop(name: str, context: dict) -> None:
    if name == '':
        print('Neviem, aký predmet chceš položiť.')
    else:
        for item in context['inventory']:
            if item['name'] == name:
                # vybrat ho z inventaru
                context['inventory'].remove(item)

                # polozit ho do miestnosti
                context['room']['items'].append(item)

                print(f'Predmet {name} si vyložil do miestnosti.')
                break
        else:
            print('Taký predmet u seba nemáš.')


def take(name: str, context: dict) -> None:
    """
    Represents the TAKE command.
    :param name: the name of item do describe
    :param room: the room object, where the player is currently in
    :param inventory: the player's inventory
    """

    room = context['room']
    inventory = context['inventory']

    if name == '':
        print('Neviem, aký predmet chceš vziať.')
    else:
        for item in room['items']:
            if item['name'] == name:
                # overit, ci je batoh plny
                # todo: zmeni konstantu na premennu
                if len(inventory) >= 2:
                    print('Batoh je plný.')

                # overit, ci sa da zobrat
                elif features.MOVABLE in item['features']:
                    # vybrat ho z roomu
                    room['items'].remove(item)

                    # vlozit do batohu
                    inventory.append(item)

                    print(f'Predmet {name} si si vložil do batohu.')
                else:
                    print('Tento predmet sa nedá zobrať.')

                break
        else:
            print('Taký predmet tu nikde nevidím.')


def examine(name: str, context: dict) -> None:
    """
    Represents the examine command.
    :param name: the name of item do describe
    :param room: the room object, where the player is currently in
    :param inventory: the player's inventory
    """

    room = context['room']
    inventory = context['inventory']

    if len(name) == 0:
        print('Neviem, aký predmet chceš preskúmať.')
    else:
        for item in room['items'] + inventory:
            if item['name'] == name:
                print(item['description'])
                break
        else:
            print('Taký predmet tu nigde nevidím.')


def use(name: str, context: dict) -> None:
    """
    Represents the examine command.
    :param name: the name of item do describe
    :param context: the game context
    """

    room = context['room']
    inventory = context['inventory']

    # nezadal meno predmetu
    if len(name) == 0:
        print('Neviem, aký predmet chceš použiť.')
        return

    # najdem predmet v miestnosti alebo inventari
    item = find_item(name, room['items'] + inventory)
    if item is None:
        print('Taký predmet tu nikde nevidím.')
        return

    # overim, ci je predmet pouzitelny
    if features.USABLE not in item['features']:
        print('Tento predmet sa nedá použiť.')
        return

    # pouzitie predmetov
    if name == 'ucebnica jazyka python':
        usages.use_textbook(item, context)

    elif name == 'kanister':
        usages.use_can(item, context)

    elif name == 'zapalky':
        usages.use_matches(item, context)

    elif name == 'hasiaci pristroj':
        usages.use_fire_extinguisher(item, context)

    else:
        print(f'Snažím sa použiť predmet {name}')


def about(name: str, context: dict) -> None:
    print('Hru spáchal v (c) 2021 mirek.')
    print('Ďalšie dobrodužstvo Indiana Jonesa. Tentokrát sa pokúsi o únik zo skladu Košického Technického múzea.')


def quit_game(name: str, context: dict) -> None:
    print('ta koncime')
    context['state'] = states.QUIT


def show_commands(name: str, context: dict) -> None:
    print('Zoznam príkazov hry:')

    for command in context['commands']:
        print(f'\t* {command["name"]} - {command["description"]}')


def west(name: str, context: dict) -> None:
    room = context['room']
    # ak sa tam neda ist, tak vypis
    if room['exits']['west'] is None:
        print('Tam sa nedá ísť.')
        return

    # najdi miestnost na zapad od tejto
    room_name = room['exits']['west']
    target_room = get_room_by_name(room_name, context['world'])

    # aktualizujeme room
    context['room'] = target_room

    # vojdeme do nej (rozhliadneme sa v nej)
    look_around(None, context)


def east(name: str, context: dict) -> None:
    room = context['room']
    # ak sa tam neda ist, tak vypis
    if room['exits']['east'] is None:
        print('Tam sa nedá ísť.')
        return

    # najdi miestnost na zapad od tejto
    room_name = room['exits']['east']
    target_room = get_room_by_name(room_name, context['world'])

    # aktualizujeme room
    context['room'] = target_room

    # vojdeme do nej (rozhliadneme sa v nej)
    look_around(None, context)


def north(name: str, context: dict) -> None:
    room = context['room']
    # ak sa tam neda ist, tak vypis
    if room['exits']['north'] is None:
        print('Tam sa nedá ísť.')
        return

    # najdi miestnost na zapad od tejto
    room_name = room['exits']['north']
    target_room = get_room_by_name(room_name, context['world'])

    # aktualizujeme room
    context['room'] = target_room

    # vojdeme do nej (rozhliadneme sa v nej)
    look_around(None, context)


def south(name: str, context: dict) -> None:
    room = context['room']
    # ak sa tam neda ist, tak vypis
    if room['exits']['south'] is None:
        print('Tam sa nedá ísť.')
        return

    # najdi miestnost na zapad od tejto
    room_name = room['exits']['south']
    target_room = get_room_by_name(room_name, context['world'])

    # aktualizujeme room
    context['room'] = target_room

    # vojdeme do nej (rozhliadneme sa v nej)
    look_around(None, context)


commands = [
    {
        'name': 'preskumaj',
        'aliases': ('examine',),
        'exec': examine,
        'description': 'zobrazí informácie o zvolenom predmete'
    },

    {
        'name': 'poloz',
        'aliases': ('drop',),
        'exec': drop,
        'description': 'vyberie predmet z batohu a položí ho do miestnosti'
    },

    {
        'name': 'koniec',
        'aliases': ('quit', 'bye', 'q', 'ukoncit'),
        'description': 'ukončí rozohratú hru',
        'exec': quit_game
    },

    {
        'name': 'o hre',
        'aliases': ('about',),
        'description': 'zobrazí informácie o hre',
        'exec': about
    },

    {
        'name': 'rozhliadni sa',
        'aliases': ('look around',),
        'description': 'zobrazí obsah miestnosti',
        'exec': look_around
    },

    {
        'name': 'inventar',
        'aliases': ('inventory', 'i'),
        'description': 'zobrazí obsah batohu',
        'exec': inventory
    },

    {
        'name': 'vezmi',
        'aliases': ('take',),
        'description': 'vezme predmet z miestnosti a vloží ho do batohu',
        'exec': take
    },

    {
        'name': 'prikazy',
        'aliases': ('commands', 'help', 'pomoc'),
        'description': 'zobrazí zoznam príkazov dostupných v hre',
        'exec': None  # commands
    },

    {
        'name': 'pouzi',
        'aliases': ('pouzit', 'use'),
        'description': 'použije zvolený predmet',
        'exec': use
    },

    {
        'name': 'zapad',
        'aliases': ('west', 'w', 'z'),
        'description': 'prejde do miestnosti na zapad',
        'exec': west
    },

    {
        'name': 'vychod',
        'aliases': ('east', 'e', 'v'),
        'description': 'prejde do miestnosti na vychod',
        'exec': east
    },

    {
        'name': 'sever',
        'aliases': ('north', 'n', 's'),
        'description': 'prejde do miestnosti na sever',
        'exec': north
    },

    {
        'name': 'juh',
        'aliases': ('south', 'j'),
        'description': 'prejde do miestnosti na juh',
        'exec': south
    },
]
                                                        features.py                                                                                         0000664 0001750 0001750 00000000027 14120125467 012677  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 MOVABLE = 1
USABLE = 2
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         helper.py                                                                                           0000664 0001750 0001750 00000000451 14120125512 012330  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 def find_item(name: str, items: list) -> dict:
    for item in items:
        if item['name'] == name:
            return item

    return None


def get_room_by_name(name: str, world: list) -> dict:
    for room in world:
        if room['name'] == name:
            return room

    return None
                                                                                                                                                                                                                       main.py                                                                                             0000664 0001750 0001750 00000004216 14120125537 012007  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 #!/usr/bin/env python3

import features
import states
import commands
import json


def parse(line: str, commands: list) -> tuple:
    for command in commands:
        for alias in command['aliases'] + (command['name'],):
            if line.startswith(alias):
                param = line.split(alias)[1].strip()
                return (command, param)

    return (None, None)


def main():
    context = {
        'commands': None,
        'inventory': None,
        'state': states.PLAYING,
        'room': None,
        'world': None
    }

    # load world
    file = open('world.json', 'r', encoding='utf-8')
    context['world'] = json.load(file)
    file.close()

    context['commands'] = commands.commands

    context['room'] = context['world'][0]

    context['inventory'] = [
        {
            'name': 'ucebnica jazyka python',
            'description': 'Mocná učebnica jazyka Python od známeho Pytonistu Jana.',
            'features': [features.MOVABLE, features.USABLE]
        }
    ]

    commands.look_around(None, context)

    # game loop
    while context['state'] == states.PLAYING:
        line = input('> ').strip().lower()

        # parse input line
        command, param = parse(line, context['commands'])
        if command is not None:
            command['exec'](param, context)
        else:
            print('Taký príkaz nepoznám.')

        # check game winning
        if context['room']['name'] == 'garden':
            context['state'] = states.WIN

    # celebrations
    if context['state'] == states.WIN:
        print("  ____                            _         _       _   _                 _ ")
        print(" / ___|___  _ __   __ _ _ __ __ _| |_ _   _| | __ _| |_(_) ___  _ __  ___| |")
        print("| |   / _ \| '_ \ / _` | '__/ _` | __| | | | |/ _` | __| |/ _ \| '_ \/ __| |")
        print("| |__| (_) | | | | (_| | | | (_| | |_| |_| | | (_| | |_| | (_) | | | \__ \_|")
        print(" \____\___/|_| |_|\__, |_|  \__,_|\__|\__,_|_|\__,_|\__|_|\___/|_| |_|___(_)")
        print("                  |___/                                                     ")

    print('...koniec...')


if __name__ == '__main__':
    main()
                                                                                                                                                                                                                                                                                                                                                                                  states.py                                                                                           0000664 0001750 0001750 00000000035 14120125555 012361  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 QUIT = 0
PLAYING = 1
WIN = 2
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   usages.py                                                                                           0000664 0001750 0001750 00000010055 14120125603 012342  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 import random

import features
from helper import find_item


def use_textbook(item, context):
    _zen_of_python = [
        'Beautiful is better than ugly.',
        'Explicit is better than implicit.',
        'Simple is better than complex.',
        'Complex is better than complicated.',
        'Flat is better than nested.',
        'Sparse is better than dense.',
        'Readability counts.',
        "Special cases aren't special enough to break the rules.",
        'Although practicality beats purity.',
        'Errors should never pass silently.',
        'Unless explicitly silenced.',
        'In the face of ambiguity, refuse the temptation to guess.',
        'There should be one-- and preferably only one --obvious way to do it.',
        "Although that way may not be obvious at first unless you're Dutch.",
        'Now is better than never.',
        'Although never is often better than *right* now.',
        "If the implementation is hard to explain, it's a bad idea.",
        'If the implementation is easy to explain, it may be a good idea.',
        "Namespaces are one honking great idea -- let's do more of those!",
    ]

    print('Zalistoval si v učebnici a dočítal si sa, že:')
    print(random.choice(_zen_of_python))


def use_can(item, context):
    room = context['room']

    # aktualizovali sme kanister
    item['description'] = 'Prázdny kanister. Po pričuchnutí je ti to jasné - bol tu benzín.'
    item['features'].remove(features.USABLE)

    # aktualizujeme dvere
    door = find_item('dvere', room['items'])

    if door is not None and door['state'] == 'zamknute':
        door['state'] = 'poliate'
        door['description'] = 'Dvere. Stále zamknuté, ale ako bonus sú poliate benzínom. ' \
                              'Je ti jasné, kto za to môže.'

        # a akcia
        print('Ta som odšroboval, rozohnal som sa a celý obsah kanistra som vylial na dvere. V '
              'miestnosti sa náhle rozľahol benzínový zápach. Proste vysoko-oktánová fajnotka.')
    else:
        print('Zahrkal som kanistrom a uistil som sa, že je stále plný.')


def use_matches(item, context):
    room = context['room']
    inventory = context['inventory']

    # musim byt v miestnosti s dverami, ktore su poliate benzinom!!!
    door = find_item('dvere', room['items'])
    if door and door['state'] == 'poliate':

        # zmazeme/vyhodime zapalky z hry (bud z miestnosti alebo z batohu)
        if item in room['items']:
            room['items'].remove(item)
        else:
            inventory.remove(item)

        # co sa stane s dverami:
        door['state'] = 'horiace'
        # zmena opisu
        door['description'] = 'Doteraz tie dvere iba voňali, teraz už aj horia. Zaujímavé, ' \
                              'čo všetko sa dnes deje v tom svete.'
        # nazov: horiace dvere
        door['name'] = 'horiace dvere'

        # akcia
        print(
            'Zahrkal si krabičkou zápaliek a jednu si z nej vytiahol. Nadýchol si sa, škrtol si a ona chytila. Usmial si sa a s úsmevom na tvári si horiacu zápalku voľne pohodil smerom k dverám. Tie neváhali a okamžite zbĺkli. Ten benzín urobil svoje.')
    else:
        print('Krabička zápaliek. Nič zaujímavé. Len na čo by som ich tak použil?')

    # todo: zapalky chytia az na tretikrat/posledna zapalka


def use_fire_extinguisher(item, context):
    room = context['room']

    # musia horiet dvere
    door = find_item('horiace dvere', room['items'])
    if door:
        # zmiznu dvere z miestnosti
        room['items'].remove(door)

        # hasiaci pristroj bude nepouzitelny
        item['features'].remove(features.USABLE)

        # zmenim mu opis na prazdny hasiaci pristroj
        item['description'] = 'Ručný hasiaci prístroj prázdny. Značka - červený.'

        # nastavim vychod z miestnosti
        room['exits']['west'] = 'garden'

        # akcia
        print(
            'Zahasil si dvere. Tie sa vplyvom tlaku hasiacej zmesy rozpadli a uvoľnili ti východ z miestnosti.')
    else:
        print('Aj by som nasnežil, ale nie je na čo.')
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   world.json                                                                                          0000664 0001750 0001750 00000003270 14120125627 012532  0                                                                                                    ustar   ubuntu                          ubuntu                                                                                                                                                                                                                 [
    {
        "name": "dungeon",
        "description": "Tmavá a stuchnutá miestnosť. Každé okno je zvonku zabarikádované a do miestnosti preniká len úzky prameň svetla. Masívne drevené dvere sú jediným východom z miestnosti.",
        "items": [
            {
                "name": "kanister",
                "description": "Kanister plný benzínu.",
                "features": [
                    1,
                    2
                ]
            },
            {
                "name": "hasiaci pristroj",
                "description": "Ručný hasiaci prístroj plný. Značka - červený.",
                "features": [
                    1,
                    2
                ]
            },
            {
                "name": "zapalky",
                "description": "Krabička zápaliek vyrobená ešte v Československu. Kvalitka.",
                "features": [
                    1,
                    2
                ],
                "total": 3
            },
            {
                "name": "dvere",
                "description": "Veľké masívne drevené dvere. Zamknuté.",
                "features": [],
                "state": "zamknute"
            }
        ],
        "exits": {
            "west": null,
            "east": null,
            "south": null,
            "north": null
        }
    },
    {
        "name": "garden",
        "description": "Pomerne zarastené hriadky niečoho, čo by sa dalo voľne nazvať záhradkou. Darí sa tu skorocelu a inej burine.",
        "items": [],
        "exits": {
            "east": "dungeon",
            "west": null,
            "north": null,
            "south": null
        }
    }
]
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        