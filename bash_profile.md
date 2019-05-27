qt-commit() { git commit -m "$@" --author "Will Saults <will@saults.io>" ;}

qt-search-featured() {
  categories=(academics arts auto business health language lifestyle outdoors remedial sports tech trades)
  for category in ${categories[@]}; do
    echo "Searching: $category"
    firebase database:get /featured/category/$@
  done ;}

qt-barf-data() {
  echo "Account:"
  firebase database:get /account/$@
  echo ""
  echo "Tutor Info:"
  firebase database:get /tutor-info/$@
  echo ""
  echo "Student Info:"
  firebase database:get /student-info/$@
  echo ""
}

qt-nuke-account() {
  read -p "You're about to nuke $@... You sure? (y/n)" CONT
  if [ "$CONT" = "y" ]; then
    echo "It shall be done!";
    firebase database:update /account/$@ --data null
    firebase database:update /tutor-info/$@ --data null
    firebase database:update /student-info/$@ --data null

    echo "";
    read -p "Featured too? (y/n)" CONT2
    if [ "$CONT2" = "y" ]; then
      read -p "Which category?" CATEGORY
      echo "Not featured anymore!";
      firebase database:update /featured/$CATEGORY/$@ --data null
    fi
  else
    echo "That's ok. Maybe next time.";
  fi
}