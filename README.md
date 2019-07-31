# RAILS INTRODUCTION COURSE - CHINOOK DB MANIPULATION
# THP

> Created on 31/07/2019 by Quentin Churet

## QUESTION ANSWERS

### EASY MODE

**Quel est le nombre total d'objets Album contenus dans la base (sans regarder les id bien sûr) ?**

*code* :
```ruby
Album.all.count
```

*answer* : 347

**Qui est l'auteur de la chanson "White Room" ?**

*code* :
```ruby
Track.find_by(title: 'White Room').artist
```

*answer* : "Eric Clapton"

**Quel groupe a sorti l'album "Use Your Illusion II" ?**

*code* :
```ruby
Album.find_by(title: 'Use Your Illusion II').artist
```

*answer* : "Guns N Roses"

### MEDIUM MODE

**Combien y a t'il d'albums dont le titre contient "Great" ?**

*code* :
```ruby
Album.where("title LIKE ?", '%Great%').count
```

*answer* : 13

**Supprime tous les albums dont le nom contient "music".**

*code* :
```ruby
Album.where('title LIKE ?', '%music%').destroy_all
```

*answer* : [#<Album id: 315, title: "Handel: Music for the Royal Fireworks (Original Ve...", artist: "English Concert & Trevor Pinnock", created_at: "2019-07-31 08:33:53", updated_at: "2019-07-31 08:33:53">, #<Album id: 319, title: "Armada: Music from the Courts of England and Spain", artist: "Fretwork", created_at: "2019-07-31 08:33:53", updated_at: "2019-07-31 08:33:53">, #<Album id: 333, title: "Purcell: Music for the Queen Mary", artist: "Equale Brass Ensemble, John Eliot Gardiner & Munic...", created_at: "2019-07-31 08:33:53", updated_at: "2019-07-31 08:33:53">, #<Album id: 346, title: "Mozart: Chamber Music", artist: "Nash Ensemble", created_at: "2019-07-31 08:33:53", updated_at: "2019-07-31 08:33:53">]

**Combien y a t'il d'albums écrits par AC/DC ?**

*code* : `Album.where(artist: 'AC/DC').count`

*answer* : 2

**Combien de chanson durent exactement 158589 millisecondes ?**

*code* :
```ruby
Track.where(duration: 158589).count
```

*answer* : 0

### HARD MODE

`puts` **en console tous les titres de AC/DC.**

*code* :
```ruby
Track.where(artist: 'AC/DC').each do |track|
  puts track.title
end
```

*answer* :
Put The Finger On You
Lets Get It Up
Inject The Venom
Snowballed
Evil Walks
C.O.D.
Breaking The Rules
Night Of The Long Knives
Spellbound
Go Down
Dog Eat Dog
Let There Be Rock
Bad Boy Boogie
Problem Child
Overdose
Hell Aint A Bad Place To Be
Whole Lotta Rosie

`puts` **en console tous les titres de l'album "Let There Be Rock".**

*code* :
```ruby
Track.where(album: 'Let There Be Rock').each do |track|
  puts track.title
end
```

*answer* :
Go Down
Dog Eat Dog
Let There Be Rock
Bad Boy Boogie
Problem Child
Overdose
Hell Aint A Bad Place To Be
Whole Lotta Rosie

**Calcule le prix total de cet album ainsi que sa durée totale.**

*code* :
```ruby
price = Track.where(album: 'Let There Be Rock').map{ |track| track.price}.reduce(&:+)
duration = Track.where(album: 'Let There Be Rock').map{ |track| track.duration}.reduce(&:+)
hash = {:price => price, :duration => duration}
```

*answer* :
{:price=>7.920000000000001, :duration=>2453259}

**Calcule le coût de l'intégralité de la discographie de "Deep Purple".**

*code* :
```ruby
deep_purple_price = Track.where(artist: 'Deep Purple').map{ |track| track.price}.reduce(&:+)
```

*answer* : 90.0899999999999

**Modifie (via une boucle) tous les titres de "Eric Clapton" afin qu'ils soient affichés avec "Britney Spears" en artist.**

*code* :
```ruby
Track.where(artist: 'Eric Clapton').each do |track|
  track.update(artist: 'Britney Spears')
end
```

*answer* : N/A
